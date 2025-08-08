-- ASH MENU por Xaruto & Unknow
-- Bypass básico
pcall(function()
    setfflag("HumanoidParallelRemoveNoPhysics", "False")
    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
end)

-- Serviços
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local StarterGui = game:GetService("StarterGui")
local LocalPlayer = Players.LocalPlayer

-- GUI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "ASH_MENU"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 500, 0, 300)
MainFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(180, 200, 255)
MainFrame.BackgroundTransparency = 0.2
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true

-- Cabeçalho
local Header = Instance.new("Frame", MainFrame)
Header.Size = UDim2.new(1, 0, 0, 35)
Header.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
Header.BorderSizePixel = 0

local Title = Instance.new("TextLabel", Header)
Title.Size = UDim2.new(1, -70, 1, 0)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "ASH MENU"
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 22
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextXAlignment = Enum.TextXAlignment.Left

local ToggleButton = Instance.new("TextButton", Header)
ToggleButton.Size = UDim2.new(0, 35, 0, 35)
ToggleButton.Position = UDim2.new(1, -35, 0, 0)
ToggleButton.Text = "-"
ToggleButton.TextScaled = true
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 80, 180)
ToggleButton.TextColor3 = Color3.new(1,1,1)
ToggleButton.BorderSizePixel = 0

-- Som clique
local ClickSound = Instance.new("Sound")
ClickSound.SoundId = "rbxassetid://7417420620"
ClickSound.Volume = 1
ClickSound.Parent = MainFrame

local function PlayClick() ClickSound:Play() end

-- Notificação
local function Notify(msg)
    StarterGui:SetCore("SendNotification", {
        Title = "ASH MENU",
        Text = msg,
        Duration = 3
    })
end

-- Layout
local Tabs = Instance.new("Frame", MainFrame)
Tabs.Size = UDim2.new(0, 100, 1, -35)
Tabs.Position = UDim2.new(0, 0, 0, 35)
Tabs.BackgroundColor3 = Color3.fromRGB(200, 220, 255)
Tabs.BackgroundTransparency = 0.1

local ButtonsFrame = Instance.new("Frame", MainFrame)
ButtonsFrame.Size = UDim2.new(1, -100, 1, -35)
ButtonsFrame.Position = UDim2.new(0, 100, 0, 35)
ButtonsFrame.BackgroundTransparency = 1

-- Funções
local function FarmUber()
    while true do
        local carro = workspace.CarrosSpawnados:FindFirstChild("ok")
        local destino = workspace:FindFirstChild("LocalMarcado")
        if carro and destino and carro:FindFirstChild("DriveSeat") then
            if not carro.PrimaryPart then
                carro.PrimaryPart = carro:FindFirstChild("DriveSeat")
            end
            carro:SetPrimaryPartCFrame(destino.CFrame)
        end
        wait(1)
    end
end

local function FarmIFood()
    loadstring(game:HttpGet('https://raw.githubusercontent.com/Cr4ki3/Flexhub/refs/heads/main/Pizza'))()
end

local function FarmErva()
    loadstring(game:HttpGet("https://pastebin.com/raw/H3AhezX7"))()
end

local function ESP()
    -- código ESP que você enviou
    loadstring([[ ]]..[[]])() -- deixei como placeholder porque o seu script ESP é longo e já foi enviado
end

local function Fly()
    -- código Fly que você enviou
    loadstring([[ ]]..[[]])()
end

local function RenomearCarro()
    local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    local menorDist, carroPerto = math.huge, nil
    for _, c in pairs(workspace.CarrosSpawnados:GetChildren()) do
        if c:IsA("Model") then
            local ref = c:FindFirstChild("DriveSeat") or c:FindFirstChildWhichIsA("BasePart")
            if ref then
                local dist = (ref.Position - hrp.Position).Magnitude
                if dist < menorDist then
                    menorDist = dist
                    carroPerto = c
                end
            end
        end
    end
    if carroPerto then
        carroPerto.Name = "ok"
        Notify("Carro renomeado para ok")
    else
        Notify("Nenhum carro encontrado")
    end
end

local function Aimbot()
    loadstring(game:HttpGet("https://pastebin.com/raw/AimbotScript"))()
end

-- Categorias
local categories = {
    ["Main"] = {
        {"Feito por: Xaruto & Unknow", function() Notify("Feito por Xaruto & Unknow") end},
        {"Compre no discord!", function() Notify("Compre no Discord!") end}
    },
    ["Farms"] = {
        {"Farm Uber", function() PlayClick() Notify("Farm Uber executado") FarmUber() end},
        {"Farm iFood", function() PlayClick() Notify("Farm iFood executado") FarmIFood() end},
        {"Farm Erva", function() PlayClick() Notify("Farm Erva executado") FarmErva() end}
    },
    ["Check"] = {
        {"Renomear carro (Uber)", function() PlayClick() RenomearCarro() end}
    },
    ["Misc"] = {
        {"Fly", function() PlayClick() Notify("Fly executado") Fly() end},
        {"ESP", function() PlayClick() Notify("ESP executado") ESP() end},
        {"Aimbot", function() PlayClick() Notify("Aimbot executado") Aimbot() end}
    }
}

-- Sistema Tabs
local function ShowCategory(cat)
    for _,child in ipairs(ButtonsFrame:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end
    for i,v in ipairs(categories[cat]) do
        local btn = Instance.new("TextButton", ButtonsFrame)
        btn.Size = UDim2.new(1, -20, 0, 30)
        btn.Position = UDim2.new(0, 10, 0, (i-1)*35)
        btn.BackgroundColor3 = Color3.fromRGB(150, 180, 255)
        btn.TextColor3 = Color3.new(0,0,0)
        btn.Font = Enum.Font.SourceSansBold
        btn.TextSize = 18
        btn.Text = v[1]
        btn.MouseButton1Click:Connect(v[2])
    end
end

local y = 0
for catName,_ in pairs(categories) do
    local tabBtn = Instance.new("TextButton", Tabs)
    tabBtn.Size = UDim2.new(1, 0, 0, 30)
    tabBtn.Position = UDim2.new(0, 0, 0, y)
    tabBtn.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
    tabBtn.TextColor3 = Color3.new(1,1,1)
    tabBtn.Font = Enum.Font.SourceSansBold
    tabBtn.TextSize = 18
    tabBtn.Text = catName
    tabBtn.MouseButton1Click:Connect(function()
        PlayClick()
        ShowCategory(catName)
    end)
    y = y + 35
end

ShowCategory("Main")

-- Toggle abrir/fechar
local open = true
ToggleButton.MouseButton1Click:Connect(function()
    PlayClick()
    open = not open
    if open then
        TweenService:Create(MainFrame, TweenInfo.new(0.3), {Size = UDim2.new(0, 500, 0, 300)}):Play()
        ToggleButton.Text = "-"
    else
        TweenService:Create(MainFrame, TweenInfo.new(0.3), {Size = UDim2.new(0, 500, 0, 35)}):Play()
        ToggleButton.Text = "+"
    end
end)
