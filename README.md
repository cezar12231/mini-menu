local players = game:GetService("Players")
local serverStorage = game:GetService("ServerStorage")

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

-- Dá os itens quando o jogador entra
players.PlayerAdded:Connect(function(jogador)
    jogador.CharacterAdded:Connect(function()
        darItens(jogador)
    end)
end)
