--wow
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Aomsing1thub/Kavo/main/README.md"))()
local Window = Library.CreateLib("TITLE", "Synapse")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Section Name")

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
                v.Main.CFrame = CFrame.new(20, 10, -5)
            end
            if v:FindFirstChild("Coal") then
                v.Coal.CFrame = CFrame.new(0, 10, 0)
            end
        elseif v.Name == "Fuel Canister" or v.Name == "Oil Barrel" or v.Name == "Morsel" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(0, 10, 0)
            end
        elseif v.Name == "Basic Egg" then
            game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
            if v:FindFirstChild("Main") then
                v.Main.CFrame = CFrame.new(1, 10, 74)
            end
        end
    end
end)

Section:NewButton("Bring Good", "Check", function() -- Buttton
    -- for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
    --     if v.Name == "Strong Axe" or v.Name == "Revolver" or v.Name == "Revolver Ammo" or v.Name == "Rifle" or v.Name == "Rifle Ammo" then
    --         game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
    --         if v:FindFirstChild("Main") then
    --             v.Main.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
    --         end
    --         -- game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
    --     end
    -- end
    -- for key, v in pairs(workspace:WaitForChild("Items"):GetChildren()) do
    --     if v.Name == "Bandage" then
    --         game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("RequestStartDraggingItem"):FireServer(v)
    --         if v:FindFirstChild("Handle") then
    --             v.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-5)
    --         end
    --         game:GetService("ReplicatedStorage"):WaitForChild("RemoteEvents"):WaitForChild("StopDraggingItem"):FireServer(v)
    --     end
    -- end
end)

Section:NewButton("Go to Camp Fire", "Check", function() -- Buttton
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 0, 10)
end)

Section:NewButton("Open all crate", "Check", function() 
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

Section:NewKeybind("KeybindText", "KeybindInfo", Enum.KeyCode.RightControl, function() -- Key OPEN/CLOSE
	Library:ToggleUI()
end)
