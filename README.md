-- HUB Chutar um Bloco da Sorte
-- Executor: Delta / Arceus X Neo

local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")

-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui

local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0,230,0,320)
Frame.Position = UDim2.new(0.35,0,0.2,0)
Frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
Frame.Active = true
Frame.Draggable = true

local UICorner = Instance.new("UICorner", Frame)

local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1,0,0,35)
Title.BackgroundTransparency = 1
Title.Text = "HUB - Chutar um Bloco da Sorte"
Title.TextColor3 = Color3.new(1,1,1)
Title.TextScaled = true

-- BOTÃO FECHAR
local Close = Instance.new("TextButton")
Close.Parent = Frame
Close.Size = UDim2.new(0,30,0,30)
Close.Position = UDim2.new(1,-35,0,3)
Close.Text = "X"
Close.BackgroundColor3 = Color3.fromRGB(255,0,0)
Close.TextColor3 = Color3.new(1,1,1)

Close.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- FUNÇÃO BOTÃO
function criarBotao(nome, posY)
    local botao = Instance.new("TextButton")
    botao.Parent = Frame
    botao.Size = UDim2.new(0,190,0,35)
    botao.Position = UDim2.new(0,20,0,posY)
    botao.BackgroundColor3 = Color3.fromRGB(40,40,40)
    botao.TextColor3 = Color3.new(1,1,1)
    botao.TextScaled = true
    botao.Text = nome
    
    local canto = Instance.new("UICorner", botao)
    
    return botao
end

-- VELOCIDADE
local speed = false
local SpeedBtn = criarBotao("Velocidade",50)

SpeedBtn.MouseButton1Click:Connect(function()
    speed = not speed
    
    while speed do
        wait()
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            player.Character.Humanoid.WalkSpeed = 50
        end
    end
    
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = 16
    end
end)

-- PULO
local jump = false
local JumpBtn = criarBotao("Pulo Alto",95)

JumpBtn.MouseButton1Click:Connect(function()
    jump = not jump
    
    while jump do
        wait()
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            player.Character.Humanoid.JumpPower = 120
        end
    end
    
    if player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.JumpPower = 50
    end
end)

-- AUTO FARM
local farm = false
local FarmBtn = criarBotao("Auto Farm",140)

FarmBtn.MouseButton1Click:Connect(function()
    farm = not farm
    
    while farm do
        wait(0.2)
        
        local char = player.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            
            for _,v in pairs(workspace:GetDescendants()) do
                if v.Name:lower():find("block") or v.Name:lower():find("bloco") then
                    char.HumanoidRootPart.CFrame = v.CFrame + Vector3.new(0,5,0)
                end
            end
        end
    end
end)

-- TELEPORTE
local TpBtn = criarBotao("TP Spawn",185)

TpBtn.MouseButton1Click:Connect(function()
    local char = player.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame = CFrame.new(0,10,0)
    end
end)

-- ANTI AFK
local AntiBtn = criarBotao("Anti AFK",230)

AntiBtn.MouseButton1Click:Connect(function()
    local vu = game:GetService("VirtualUser")
    
    player.Idled:Connect(function()
        vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        wait(1)
        vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
    end)
end)

-- ABRIR / FECHAR MENU
local Toggle = Instance.new("TextButton")
Toggle.Parent = ScreenGui
Toggle.Size = UDim2.new(0,100,0,35)
Toggle.Position = UDim2.new(0,10,0,10)
Toggle.Text = "Abrir/Fechar"
Toggle.BackgroundColor3 = Color3.fromRGB(0,0,0)
Toggle.TextColor3 = Color3.new(1,1,1)

local aberto = true

Toggle.MouseButton1Click:Connect(function()
    aberto = not aberto
    Frame.Visible = aberto
end)
