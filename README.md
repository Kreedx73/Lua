-- Painel Avançado com Categorias, Comandos RP, Jogos de Farm e Imagem de Fundo
-- Cole em seu executor, substitua o link da imagem pela sua imagem hospedada

local IMAGEM_FUNDO = "https://i.imgur.com/CdJ6Yq8.jpg" -- Substitua pelo link direto da imagem

local plr = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", plr:WaitForChild("PlayerGui"))
gui.Name = "PainelKreedxMD"

local frame = Instance.new("Frame", gui)
frame.BackgroundTransparency = 1
frame.Position = UDim2.new(0.25,0,0.2,0)
frame.Size = UDim2.new(0,400,0,350)
frame.Active = true
frame.Draggable = true

local fundo = Instance.new("ImageLabel", frame)
fundo.Image = IMAGEM_FUNDO
fundo.Size = UDim2.new(1,0,1,0)
fundo.BackgroundTransparency = 1

local title = Instance.new("TextLabel", frame)
title.Text = "KreedxMD Painel"
title.Font = Enum.Font.GothamBold
title.TextColor3 = Color3.fromRGB(255,255,255)
title.BackgroundTransparency = 1
title.Size = UDim2.new(1,0,0,40)
title.TextSize = 28
title.ZIndex = 2

local closeBtn = Instance.new("TextButton", frame)
closeBtn.Text = "X"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextColor3 = Color3.new(1,0.2,0.2)
closeBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
closeBtn.Position = UDim2.new(0.94,0,0.02,0)
closeBtn.Size = UDim2.new(0,22,0,22)
closeBtn.TextSize = 16
closeBtn.ZIndex = 2

local minusBtn = Instance.new("TextButton", frame)
minusBtn.Text = "-"
minusBtn.Font = Enum.Font.GothamBold
minusBtn.TextColor3 = Color3.new(1,1,1)
minusBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
minusBtn.Position = UDim2.new(0.89,0,0.02,0)
minusBtn.Size = UDim2.new(0,22,0,22)
minusBtn.TextSize = 16
minusBtn.ZIndex = 2

local plusBtn = Instance.new("TextButton", frame)
plusBtn.Text = "+"
plusBtn.Font = Enum.Font.GothamBold
plusBtn.TextColor3 = Color3.new(1,1,1)
plusBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
plusBtn.Position = UDim2.new(0.84,0,0.02,0)
plusBtn.Size = UDim2.new(0,22,0,22)
plusBtn.TextSize = 16
plusBtn.ZIndex = 2

local categorias = {
    ["RPs"] = {
        "otimizacao", -- otimiza o jogo
        "view (player)", -- ver onde está o player
        "god me", -- imortal
        "invisible", -- invisível
    },
    ["Jogos de Farm"] = {
        "auto farm", -- identifica NPCs, mata usando estilo ou habilidade
    }
}

local categoriaAtual = "RPs"

local categoriaBox = Instance.new("Frame", frame)
categoriaBox.BackgroundTransparency = 0.5
categoriaBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
categoriaBox.Position = UDim2.new(0.05,0,0.15,0)
categoriaBox.Size = UDim2.new(0,110,0,150)
categoriaBox.ZIndex = 2

local catTitle = Instance.new("TextLabel", categoriaBox)
catTitle.Text = "Categorias"
catTitle.Font = Enum.Font.GothamBold
catTitle.TextColor3 = Color3.new(0.8,0.8,1)
catTitle.BackgroundTransparency = 1
catTitle.Size = UDim2.new(1,0,0,22)
catTitle.TextSize = 16
catTitle.ZIndex = 3

local catBtns = {}
local catY = 28
for cat, _ in pairs(categorias) do
    local btn = Instance.new("TextButton", categoriaBox)
    btn.Text = cat
    btn.Font = Enum.Font.Gotham
    btn.TextColor3 = Color3.fromRGB(200,200,255)
    btn.BackgroundColor3 = Color3.fromRGB(60,60,90)
    btn.Position = UDim2.new(0,0,0,catY)
    btn.Size = UDim2.new(1,0,0,24)
    btn.TextSize = 15
    btn.ZIndex = 3
    btn.MouseButton1Click:Connect(function()
        categoriaAtual = cat
        atualizarComandos()
    end)
    catBtns[#catBtns+1] = btn
    catY = catY + 26
end

local comandosBox = Instance.new("Frame", frame)
comandosBox.BackgroundTransparency = 0.5
comandosBox.BackgroundColor3 = Color3.fromRGB(30,30,30)
comandosBox.Position = UDim2.new(0.33,0,0.15,0)
comandosBox.Size = UDim2.new(0,240,0,150)
comandosBox.ZIndex = 2

local comandosLbl = Instance.new("TextLabel", comandosBox)
comandosLbl.Text = "Comandos"
comandosLbl.Font = Enum.Font.GothamBold
comandosLbl.TextColor3 = Color3.new(1,1,1)
comandosLbl.BackgroundTransparency = 1
comandosLbl.Size = UDim2.new(1,0,0,22)
comandosLbl.TextSize = 16
comandosLbl.ZIndex = 3

local comandoBtns = {}
function atualizarComandos()
    for _, btn in pairs(comandoBtns) do btn:Destroy() end
    comandoBtns = {}
    local y = 28
    for _, cmd in ipairs(categorias[categoriaAtual]) do
        local btn = Instance.new("TextButton", comandosBox)
        btn.Text = cmd
        btn.Font = Enum.Font.Gotham
        btn.TextColor3 = Color3.fromRGB(255,200,200)
        btn.BackgroundColor3 = Color3.fromRGB(80,40,80)
        btn.Position = UDim2.new(0,0,0,y)
        btn.Size = UDim2.new(1,0,0,22)
        btn.TextSize = 14
        btn.ZIndex = 3
        btn.MouseButton1Click:Connect(function()
            executarComando(cmd)
        end)
        comandoBtns[#comandoBtns+1] = btn
        y = y + 24
    end
end
atualizarComandos()

-- CMD Box
local cmdbox = Instance.new("TextBox", frame)
cmdbox.PlaceholderText = "Digite comando ex: view joao"
cmdbox.Font = Enum.Font.Gotham
cmdbox.TextColor3 = Color3.fromRGB(255,255,255)
cmdbox.BackgroundColor3 = Color3.fromRGB(35,35,50)
cmdbox.Position = UDim2.new(0.07,0,0.75,0)
cmdbox.Size = UDim2.new(0,330,0,34)
cmdbox.TextSize = 16
cmdbox.ZIndex = 2

local status = Instance.new("TextLabel", frame)
status.Text = "Pronto!"
status.Font = Enum.Font.Gotham
status.TextColor3 = Color3.fromRGB(255,255,255)
status.BackgroundTransparency = 1
status.Position = UDim2.new(0.07,0,0.88,0)
status.Size = UDim2.new(0,320,0,30)
status.TextSize = 15
status.ZIndex = 2

-- Funções dos comandos (codifique cada ação aqui)
function executarComando(cmd)
    status.Text = "Executando: " .. tostring(cmd)
    if cmd == "otimizacao" then
        -- Otimização do jogo
        local lighting = game:GetService("Lighting")
        local terrain = workspace:FindFirstChildOfClass("Terrain")
        lighting.GlobalShadows = false
        lighting.FogEnd = 100000
        lighting.Brightness = 1
        lighting.OutdoorAmbient = Color3.new(1,1,1)
        lighting.Ambient = Color3.new(1,1,1)
        for _, v in pairs(lighting:GetChildren()) do
            if v:IsA("PostEffect") then v:Destroy() end
        end
        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Decal") or obj:IsA("Texture") then obj.Transparency = 1 end
            if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or obj:IsA("Smoke") or obj:IsA("Fire") or obj:IsA("Explosion") then obj.Enabled = false end
        end
        if terrain then
            terrain.WaterWaveSize = 0
            terrain.WaterWaveSpeed = 0
            terrain.WaterReflectance = 0
            terrain.WaterTransparency = 1
        end
        status.Text = "Otimização aplicada!"
    elseif cmd:match("^view") then
        local target = cmd:match("^view%s+(%w+)$")
        if target then
            local targetPlr = game.Players:FindFirstChild(target)
            if targetPlr and targetPlr.Character and targetPlr.Character:FindFirstChild("HumanoidRootPart") then
                plr.Character:MoveTo(targetPlr.Character.HumanoidRootPart.Position)
                status.Text = "Movido para " .. target
            else
                status.Text = "Player não encontrado!"
            end
        else
            status.Text = "Comando: view [player]"
        end
    elseif cmd == "god me" then
        if plr.Character and plr.Character:FindFirstChildOfClass("Humanoid") then
            plr.Character:FindFirstChildOfClass("Humanoid").MaxHealth = math.huge
            plr.Character:FindFirstChildOfClass("Humanoid").Health = math.huge
            status.Text = "Modo imortal ativado!"
        else
            status.Text = "Personagem não encontrado!"
        end
    elseif cmd == "invisible" then
        if plr.Character then
            for _, v in pairs(plr.Character:GetDescendants()) do
                if v:IsA("BasePart") then
                    v.Transparency = 1
                elseif v:IsA("Decal") then
                    v.Transparency = 1
                end
            end
            status.Text = "Você está invisível!"
        else
            status.Text = "Personagem não encontrado!"
        end
    elseif cmd == "auto farm" then
        status.Text = "Auto Farm iniciado!"
        -- Exemplo básico: identificar NPCs (ajuste conforme o jogo)
        local npcs = {}
        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Model") and obj:FindFirstChildOfClass("Humanoid") and not game.Players:FindFirstChild(obj.Name) then
                table.insert(npcs, obj)
            end
        end
        for _, npc in ipairs(npcs) do
            if plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                plr.Character:MoveTo(npc.HumanoidRootPart.Position)
                npc:FindFirstChildOfClass("Humanoid").Health = 0
                wait(0.5)
            end
        end
        status.Text = "Auto Farm concluído!"
    else
        status.Text = "Comando não reconhecido!"
    end
end

cmdbox.FocusLost:Connect(function(enter)
    if enter and cmdbox.Text ~= "" then
        executarComando(cmdbox.Text)
        cmdbox.Text = ""
    end
end)

-- Funções dos botões de painel
closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)
local painelMin = false
minusBtn.MouseButton1Click:Connect(function()
    if not painelMin then
        frame.Size = UDim2.new(0,100,0,40)
        fundo.Size = UDim2.new(1,0,1,0)
        painelMin = true
    end
end)
plusBtn.MouseButton1Click:Connect(function()
    if painelMin then
        frame.Size = UDim2.new(0,400,0,350)
        fundo.Size = UDim2.new(1,0,1,0)
        painelMin = false
    end
end)

-- Fim do Script Painel KreedxMD Avançado
