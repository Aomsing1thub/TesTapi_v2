local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Aomsing1thub/Kavo/main/README.md"))()
local Window = Library.CreateLib("TITLE", "Synapse")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Section Name")

Section:NewButton("Copy CFrame", "Check", function() -- Buttton
    setclipboard(tostring(game.Players.LocalPlayer.Character.HumanoidRootPart.Position))
end)

Section:NewButton("Fill Fuel", "Check", function() -- Buttton
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
                -- v.Main.CFrame = CFrame.new(0, 10, 0)
                v.Main.CFrame = CFrame.new(20, 15, -5)
            end
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

Section:NewKeybind("Go to Camp Fire", "KeybindInfo", Enum.KeyCode.Z, function() -- Key OPEN/CLOSE
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 5, 10)
end)

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.X, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)




--
