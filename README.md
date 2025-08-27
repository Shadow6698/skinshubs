-- Carregar Rayfield
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "Avatar Hub - Rayfield",
    LoadingTitle = "Carregando Avatares 3D",
    LoadingSubtitle = "by Nightmare",
    ConfigurationSaving = { Enabled = false },
    Discord = { Enabled = false },
    KeySystem = false,
})

-- Criar aba Skins 3D
local Tab = Window:CreateTab("Skins 3D", 4483362458)

local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Funções
local function EquiparAvatarPorID(avatarID, nome)
    local args = { avatarID }
    local success, result = pcall(function()
        return ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("Wear"):InvokeServer(unpack(args))
    end)
    if success then
        Rayfield:Notify({
            Title = "Avatar Equipado",
            Content = nome .. " equipado com sucesso!",
            Duration = 5
        })
    else
        Rayfield:Notify({
            Title = "Erro",
            Content = "Falha ao equipar " .. nome,
            Duration = 5
        })
    end
end

local function EquiparPartesCorpo(partes)
    local args = { partes }
    local success, result = pcall(function()
        return ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("ChangeCharacterBody"):InvokeServer(unpack(args))
    end)
    if success then
        Rayfield:Notify({
            Title = "Avatar Resetado",
            Content = "Partes aplicadas com sucesso!",
            Duration = 5
        })
    else
        Rayfield:Notify({
            Title = "Erro",
            Content = "Falha ao aplicar partes",
            Duration = 5
        })
    end
end

-- Lista de avatares
local Avatares = {
    {124948425515124,"Gato de Manga"},
    {117098257036480,"Tung Saur"},
    {99459753608381,"Tralaleiro"},
    {123609977175226,"Monstro S.A"},
    {80468697076178,"Trenzinho"},
    {11941741105,"Dino"},
    {15742966010,"Pou Idoso"},
    {77013984520332,"Coco/Boxt@"},
    {71797333686800,"Coelho"},
    {73215892129281,"Hipopótamo"},
    {108557570415453,"Ratatui"},
    {71251793812515,"Galinha"},
    {92979204778377,"Peppa Pig"},
    {94944293759578,"Pinguim"},
    {87442757321244,"Sid"},
    {111436158728716,"Puga Grande"},
    {120960401202173,"SHREK AMALDIÇOADO"},
    {108052868536435,"Mosquito Grande"},
    {106596990206151,"Noob Invertido"},
    {135132836238349,"Pato(a)"},
    {18656467256,"Cachorro Chihuahua"},
    {18994959003,"Gato Sla"},
    {77506186615650,"Gato Fei"},
    {18234669337,"Impostor"},
    {75183593514657,"Simon Amarelo"},
    {76155710249925,"Simon Azul"}
}

-- Lista de corpos
local Corpos = {
    {"Mini REPO",{117101023704825,125767940563838,137301494386930,87357384184710,133391239416999,111818794467824}},
    {"Mini Garanhão",{124355047456535,120507500641962,82273782655463,113625313757230,109182039511426,0}},
    {"Stick",{14731384498,14731377938,14731377894,14731377875,14731377941,14731382899}},
    {"Chunky-Bug",{15527827600,15527827578,15527831669,15527836067,15527827184,15527827599}},
    {"Cursed-Spider",{134555168634906,100269043793774,125607053187319,122504853343598,95907982259204,91289185840375}},
    {"Possessed-Horror",{122800511983371,132465361516275,125155800236527,83070163355072,102906187256945,78311422507297}}
}

-- Criar botões para cada avatar
for _, dados in ipairs(Avatares) do
    local id, nome = dados[1], dados[2]
    Tab:CreateButton({
        Name = nome,
        Callback = function()
            EquiparAvatarPorID(id, nome)
        end
    })
end

-- Criar seção para corpos
local SectionCorpos = Tab:CreateSection("Avatares de Corpo (resetam o avatar)")

-- Criar botões para cada corpo
for _, dados in ipairs(Corpos) do
    local nome, partes = dados[1], dados[2]
    Tab:CreateButton({
        Name = nome,
        Callback = function()
            EquiparPartesCorpo(partes)
        end
    })
end
