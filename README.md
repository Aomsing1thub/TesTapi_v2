local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Aomsing1thub/Kavo/main/README.md"))()
local Window = Library.CreateLib("TITLE", "Synapse")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Section Name")

Section:NewButton("Copy CFrame", "Check", function() -- Buttton
    setclipboard(tostring(game.Players.LocalPlayer.Character.HumanoidRootPart.Position))
end)

Section:NewButton("Fill Bench", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Log" 
        or v.Name == "Coal" 
        or v.Name == "Broken Fan" 
        or v.Name == "Tyre" 
        or v.Name == "Broken Microwave" 
        or v.Name == "Bolt" 
        or v.Name == "Old Radio" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(20, 15, -5)
            end
        elseif v.Name == "Basic Egg" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(1, 15, 74)
            end
        end
    end
end)

Section:NewButton("Fill Fuel", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Coal" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Coal") then
                v.Coal.CFrame = CFrame.new(0, 15, 0)
            end
        elseif v.Name == "Fuel Canister" or v.Name == "Oil Barrel" or v.Name == "Morsel" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(0, 15, 0)
            end
        elseif v.Name == "Basic Egg" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(1, 15, 74)
            end
        end
    end
end)

Section:NewButton("Bring Armor", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Iron Body" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring Bandage", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Bandage" or v.Name == "MedKit" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Handle") then
                v.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring All Blueprint", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if string.find(v.Name,"Blueprint") then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring All Sack", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if string.find(v.Name,"Sack") then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Sack") then
                v.Sack.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring Strong Flashlight", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Strong Flashlight" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring Impact Grenade", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Impact Grenade" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Bring Weapon", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Strong Axe" or v.Name == "Revolver" or v.Name == "Revolver Ammo" or v.Name == "Rifle" or v.Name == "Rifle Ammo" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
            end
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
        end
    end
end)

Section:NewButton("Open all crate", "Check", function() -- Buttton
    for key, v in pairs(workspace:WaitForChild("Items"):GetDescendants()) do
        if v:IsA("ProximityPrompt") then
            fireproximityprompt(v)
            wait()
        end
    end
end)

Section:NewToggle("Hide Frog", "ToggleInfo", function(state)
    a1 = state
    if not a1 then
    end
end)

Section:NewToggle("Auto Cut tree", "ToggleInfo", function(state)
    a2 = state
    if not a2 then
    end
end)

spawn(function()
while wait() do
if a1 then
pcall(function()
    function Touch(T2)
    firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,T2,0)
    firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,T2,1)
    end

    for key, v in pairs(workspace.Map.Boundaries:GetChildren()) do
        if v:FindFirstChild("TouchInterest") then
            Touch(v)
        end
    end
end)
end
end
end)

spawn(function()
while wait() do
if a2 then
pcall(function()
    for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
        if v.Name == "Strong Axe" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestHotbarItem"):InvokeServer(v)
        end
    end

    for i,v in pairs (game:GetService("Players").LocalPlayer.Inventory:GetChildren()) do
        if string.find(v.Name,"Axe") then
            Mytool = v
        end
    end

    local args = {
    "FireAllClients",
    Mytool
    }
    game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("EquipItemHandle"):FireServer(unpack(args))

    for key, v in pairs(workspace.Map.Foliage:GetChildren()) do
        if v.Name == "Small Tree" and a2 then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.Trunk.CFrame * CFrame.new(0,10,0)
            wait(.1)
            local args = {
                v,
                Mytool,
                "27_2777604486",
                CFrame.new(-52.84754943847656, 3.8810336589813232, 36.91767501831055, -0.4882603883743286, 8.754180491621355e-09, 0.8726980090141296, -3.554958993845503e-08, 1, -2.99205886733489e-08, -0.8726980090141296, -4.5633093748165265e-08, -0.4882603883743286)
            }
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("ToolDamageObject"):InvokeServer(unpack(args))
        end
    end
end)
end
end
end)

Section:NewKeybind("Go to Camp Fire", "KeybindInfo", Enum.KeyCode.Z, function() -- Key OPEN/CLOSE
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 5, 10)
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.X, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)




--
