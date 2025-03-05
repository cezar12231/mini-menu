local players = game:GetService("Players")
local serverStorage = game:GetService("ServerStorage")

-- Criando a ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Criando o Frame (Painel)
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 150)
frame.Position = UDim2.new(0.5, -100, 0.5, -75)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
frame.Parent = screenGui

-- Criando o botão para dar armas
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 180, 0, 50)
button.Position = UDim2.new(0.5, -90, 0.5, -25)
button.Text = "Receber Armas"
button.Parent = frame

-- Lista de armas para dar ao jogador
local armas = {"AK47", "IA2", "UZI"}

local function darItens(jogador)
    local character = jogador.Character or jogador.CharacterAdded:Wait()
    local backpack = jogador:FindFirstChild("Backpack")
    
    if backpack then
        for _, arma in ipairs(armas) do
            local item = serverStorage:FindFirstChild(arma)
            if item then
                local clone = item:Clone()
                clone.Parent = backpack
            end
        end
    end
end

-- Dá os itens quando o botão é pressionado
button.MouseButton1Click:Connect(function()
    local jogador = players.LocalPlayer
    darItens(jogador)
end)
