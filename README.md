-- Lib UI "Kavo"
local l = loadstring(game:HttpGet("https://raw.githubusercontent.com/Kavo-hub/Kavo-UI-Library/main/source.lua"))()
local w = l.CreateLib("LPS Interface", "DarkTheme")
local t = w:NewTab("Interface")
local s = t:NewSection("Modulos")

-- Variáveis internas (não chamativas)
local a, b = false, false
local lp = game:GetService("Players").LocalPlayer
local hrp = lp.Character and lp.Character:FindFirstChild("HumanoidRootPart")

if not hrp then
    lp.CharacterAdded:Wait()
    hrp = lp.Character:WaitForChild("HumanoidRootPart")
end

-- Função central anônima (raridade = "Mythic" ou "Legendary")
local function r(e)
    while (e == "Mythic" and a) or (e == "Legendary" and b) do
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("Model") and v:FindFirstChildWhichIsA("ProximityPrompt") then
                if string.find(string.lower(v.Name), string.lower(e)) then
                    pcall(function()
                        hrp.CFrame = v:GetModelCFrame() + Vector3.new(0, 3, 0)
                        fireproximityprompt(v:FindFirstChildWhichIsA("ProximityPrompt"))
                    end)
                    task.wait(0.25)
                end
            end
        end
        task.wait(0.5)
    end
end

-- Toggle para tipo 1
s:NewToggle("Modulo: X1", "Executar ação discreta", function(v)
    a = v
    if v then task.spawn(function() r("Mythic") end) end
end)

-- Toggle para tipo 2
s:NewToggle("Modulo: X2", "Executar ação discreta", function(v)
    b = v
    if v then task.spawn(function() r("Legendary") end) end
end)
