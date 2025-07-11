local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local highlights = {}

-- Função para criar o Highlight vermelho em todos jogadores (menos você)
local function ativarHighlight()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            if not player.Character:FindFirstChild("Highlight") then
                local highlight = Instance.new("Highlight")
                highlight.Name = "Highlight"
                highlight.FillColor = Color3.fromRGB(255,0,0)
                highlight.OutlineColor = Color3.fromRGB(255,0,0)
                highlight.FillTransparency = 0.5
                highlight.OutlineTransparency = 0
                highlight.Parent = player.Character
                highlights[player.Character] = highlight
            end
        end
    end
end

-- Interface
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MinhaInterface"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 250, 0, 120)
mainFrame.Position = UDim2.new(0, 30, 0, 30)
mainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = ScreenGui

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 40)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "Minha Interface"
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextSize = 24
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Parent = mainFrame

local highlightBtn = Instance.new("TextButton")
highlightBtn.Size = UDim2.new(0.8, 0, 0, 35)
highlightBtn.Position = UDim2.new(0.1, 0, 0, 55)
highlightBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113) -- Verde
highlightBtn.Text = "Ativar Highlight"
highlightBtn.Font = Enum.Font.SourceSansBold
highlightBtn.TextSize = 18
highlightBtn.TextColor3 = Color3.fromRGB(255,255,255)
highlightBtn.Parent = mainFrame

highlightBtn.MouseButton1Click:Connect(function()
    ativarHighlight()
end)
