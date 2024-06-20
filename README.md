full stack developer 
(c++ & lua ) 


--basic esp.
local function createESP(player)
    local character = player.Character or player.CharacterAdded:Wait()
    
    for _, part in ipairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            local box = Instance.new("BoxHandleAdornment")
            box.Adornee = part
            box.Size = part.Size
            box.Transparency = 0.5
            box.Color3 = Color3.new(1, 0, 0)  -- Red color
            box.AlwaysOnTop = true
            box.ZIndex = 10
            box.Parent = part
        end
    end
end

-- Function to remove ESP from a character
local function removeESP(player)
    local character = player.Character
    if character then
        for _, part in ipairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                for _, adornment in ipairs(part:GetChildren()) do
                    if adornment:IsA("BoxHandleAdornment") then
                        adornment:Destroy()
                    end
                end
            end
        end
    end
end


local function toggleESP(player)
    if player.Character then
        if player.Character:FindFirstChildOfClass("BoxHandleAdornment") then
            removeESP(player)
        else
            createESP(player)
        end
    end
end


local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

UserInputService.InputBegan:Connect(function(input, processed)
    if not processed and input.KeyCode == Enum.KeyCode.E then
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer then
                toggleESP(player)
            end
        end
    end
end)
