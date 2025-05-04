# Script-Nunes
Script/exploit for Roblox
-- Nome ESP/ESP básico
local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")

-- Cria uma pasta para armazenar os destaques
local storage = Instance.new("Folder", CoreGui)
storage.Name = "ESP_Highlights"

-- Configurações de aparência
local fillColor = Color3.fromRGB(175, 25, 255)
local outlineColor = Color3.fromRGB(255, 255, 255)

-- Função para aplicar ESP em um jogador
local function addHighlight(player)
    if player.Character then
        local highlight = Instance.new("Highlight")
        highlight.Name = player.Name
        highlight.FillColor = fillColor
        highlight.OutlineColor = outlineColor
        highlight.FillTransparency = 0.5
        highlight.OutlineTransparency = 0
        highlight.Adornee = player.Character
        highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
        highlight.Parent = storage

        -- Atualiza quando o personagem é recriado
        player.CharacterAdded:Connect(function(char)
            highlight.Adornee = char
        end)
    end
end

-- Aplica ESP em todos os jogadores existentes
for _, player in pairs(Players:GetPlayers()) do
    if player ~= Players.LocalPlayer then
        addHighlight(player)
    end
end

-- Aplica ESP em novos jogadores que entrarem
Players.PlayerAdded:Connect(function(player)
    if player ~= Players.LocalPlayer then
        addHighlight(player)
    end
end)
