-- Carregar Fluent
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

-- Criar Janela
local Window = Fluent:CreateWindow({
    Title = "TPs Rápido",
    TabWidth = 160,
    Size = UDim2.fromOffset(500, 400),
    Theme = "Dark"
})

-- Aba de Teleportes
local Tab = Window:AddTab({ Title = "TPs" })

-- Função de teleporte
local function teleportTo(pos)
    local char = game.Players.LocalPlayer.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame = CFrame.new(pos)
    end
end

-- Pontos definidos
local pontoA = Vector3.new(129.500549, 124.999977, -4.395827)
local pontoB = Vector3.new(136.965255, 123.070671, -31.900058)

-- Controle AutoTP
local autoTP = false

-- Thread de AutoTP
task.spawn(function()
    while true do
        if autoTP then
            teleportTo(pontoA)
            teleportTo(pontoB)
        end
        task.wait() -- sem delay visível, mas necessário para não travar o jogo
    end
end)

-- Toggle
Tab:AddToggle("AutoTP", { Title = "AutoTP A <-> B" }):OnChanged(function(val)
    autoTP = val
end)

Window:SelectTab(1)
