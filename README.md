repeat task.wait() until game:IsLoaded()

local scanned = {}
local total = 0

print("🔎 Advanced Remote Scanner Started")

local function checkRemote(obj)
    if obj:IsA("RemoteEvent") or obj:IsA("RemoteFunction") then
        if not scanned[obj] then
            scanned[obj] = true
            total += 1

            print("📡 Remote Found")
            print("Name:", obj.Name)
            print("Type:", obj.ClassName)
            print("Path:", obj:GetFullName())
            print("-----------------------")
        end
    end
end

-- scan existing
for _,v in pairs(game:GetDescendants()) do
    checkRemote(v)
end

-- monitor new objects
game.DescendantAdded:Connect(function(obj)
    checkRemote(obj)
end)

print("✅ Scanner running | Total:", total)
