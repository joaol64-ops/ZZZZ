local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "ZzzUI"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

-- 🔳 BOTÃO Z
local openBtn = Instance.new("TextButton", gui)
openBtn.Size = UDim2.new(0,60,0,60)
openBtn.Position = UDim2.new(0,20,0.5,0)
openBtn.BackgroundColor3 = Color3.fromRGB(30,30,30)
openBtn.Text = "Z"
openBtn.Font = Enum.Font.GothamBlack
openBtn.TextSize = 28
openBtn.TextColor3 = Color3.fromRGB(255,255,255)
openBtn.Active = true
openBtn.Draggable = true

Instance.new("UICorner", openBtn).CornerRadius = UDim.new(0,10)

local strokeBtn = Instance.new("UIStroke", openBtn)
strokeBtn.Color = Color3.fromRGB(150,150,150)
strokeBtn.Thickness = 2

-- 🧱 PAINEL
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,280,0,510)
frame.Position = UDim2.new(0.5,-140,0.5,-255)
frame.BackgroundColor3 = Color3.fromRGB(0,0,0)
frame.Visible = false
frame.Active = true
frame.Draggable = true

Instance.new("UICorner", frame).CornerRadius = UDim.new(0,12)

local stroke = Instance.new("UIStroke", frame)
stroke.Color = Color3.fromRGB(150,150,150)
stroke.Thickness = 2

-- TÍTULO
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,-40,0,30)
title.Position = UDim2.new(0,10,0,0)
title.Text = "Pvp Laboratório"
title.Font = Enum.Font.GothamBold
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundTransparency = 1
title.TextXAlignment = Enum.TextXAlignment.Left

-- ❌ FECHAR
local close = Instance.new("TextButton", frame)
close.Size = UDim2.new(0,30,0,30)
close.Position = UDim2.new(1,-30,0,0)
close.Text = "X"
close.BackgroundTransparency = 1
close.TextColor3 = Color3.new(1,1,1)

-- 🔘 TOGGLE
local function criarToggle(nome, posY)
	local bg = Instance.new("Frame", frame)
	bg.Size = UDim2.new(1,-20,0,40)
	bg.Position = UDim2.new(0,10,0,posY)
	bg.BackgroundColor3 = Color3.fromRGB(40,40,40)

	Instance.new("UICorner", bg).CornerRadius = UDim.new(0,8)

	local txt = Instance.new("TextLabel", bg)
	txt.Size = UDim2.new(0.6,0,1,0)
	txt.Position = UDim2.new(0,10,0,0)
	txt.Text = nome
	txt.Font = Enum.Font.GothamBold
	txt.TextColor3 = Color3.new(1,1,1)
	txt.BackgroundTransparency = 1
	txt.TextXAlignment = Enum.TextXAlignment.Left

	local toggle = Instance.new("TextButton", bg)
	toggle.Size = UDim2.new(0,50,0,25)
	toggle.Position = UDim2.new(1,-60,0.5,-12)
	toggle.Text = ""
	toggle.BackgroundColor3 = Color3.fromRGB(80,80,80)

	Instance.new("UICorner", toggle).CornerRadius = UDim.new(1,0)

	local circle = Instance.new("Frame", toggle)
	circle.Size = UDim2.new(0,20,0,20)
	circle.Position = UDim2.new(0,2,0.5,-10)
	circle.BackgroundColor3 = Color3.new(1,1,1)

	Instance.new("UICorner", circle).CornerRadius = UDim.new(1,0)

	local state = false

	toggle.MouseButton1Click:Connect(function()
		state = not state

		if state then
			toggle.BackgroundColor3 = Color3.fromRGB(0,170,0)
			circle.Position = UDim2.new(1,-22,0.5,-10)
		else
			toggle.BackgroundColor3 = Color3.fromRGB(80,80,80)
			circle.Position = UDim2.new(0,2,0.5,-10)
		end
	end)

	return function() return state end
end

-- 🔘 SLIDER (para velocidade)
local function criarSlider(nome, posY, min, max, padrao)
	local bg = Instance.new("Frame", frame)
	bg.Size = UDim2.new(1,-20,0,60)
	bg.Position = UDim2.new(0,10,0,posY)
	bg.BackgroundColor3 = Color3.fromRGB(40,40,40)
	
	Instance.new("UICorner", bg).CornerRadius = UDim.new(0,8)
	
	local txt = Instance.new("TextLabel", bg)
	txt.Size = UDim2.new(1,0,0,20)
	txt.Position = UDim2.new(0,10,0,5)
	txt.Text = nome
	txt.Font = Enum.Font.GothamBold
	txt.TextColor3 = Color3.new(1,1,1)
	txt.BackgroundTransparency = 1
	txt.TextXAlignment = Enum.TextXAlignment.Left
	
	local valorTxt = Instance.new("TextLabel", bg)
	valorTxt.Size = UDim2.new(0,50,0,20)
	valorTxt.Position = UDim2.new(1,-60,0,5)
	valorTxt.Text = tostring(padrao)
	valorTxt.Font = Enum.Font.GothamBold
	valorTxt.TextColor3 = Color3.fromRGB(0,170,0)
	valorTxt.BackgroundTransparency = 1
	
	local sliderBg = Instance.new("Frame", bg)
	sliderBg.Size = UDim2.new(1,-20,0,4)
	sliderBg.Position = UDim2.new(0,10,0,35)
	sliderBg.BackgroundColor3 = Color3.fromRGB(80,80,80)
	Instance.new("UICorner", sliderBg).CornerRadius = UDim.new(1,0)
	
	local sliderFill = Instance.new("Frame", sliderBg)
	sliderFill.Size = UDim2.new((padrao - min) / (max - min), 0, 1, 0)
	sliderFill.BackgroundColor3 = Color3.fromRGB(0,170,0)
	Instance.new("UICorner", sliderFill).CornerRadius = UDim.new(1,0)
	
	local sliderBtn = Instance.new("TextButton", sliderBg)
	sliderBtn.Size = UDim2.new(0,12,0,12)
	sliderBtn.Position = UDim2.new((padrao - min) / (max - min), -0.5, 0.5, -6)
	sliderBtn.BackgroundColor3 = Color3.fromRGB(255,255,255)
	sliderBtn.Text = ""
	Instance.new("UICorner", sliderBtn).CornerRadius = UDim.new(1,0)
	
	local valor = padrao
	local dragging = false
	
	sliderBtn.MouseButton1Down:Connect(function()
		dragging = true
	end)
	
	UserInputService.InputEnded:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 then
			dragging = false
		end
	end)
	
	RunService.RenderStepped:Connect(function()
		if dragging then
			local mousePos = UserInputService:GetMouseLocation()
			local sliderAbsPos = sliderBg.AbsolutePosition
			local sliderWidth = sliderBg.AbsoluteSize.X
			
			local percent = (mousePos.X - sliderAbsPos.X) / sliderWidth
			percent = math.clamp(percent, 0, 1)
			
			valor = min + (max - min) * percent
			valor = math.floor(valor)
			
			sliderFill.Size = UDim2.new(percent, 0, 1, 0)
			sliderBtn.Position = UDim2.new(percent, -6, 0.5, -6)
			valorTxt.Text = tostring(valor)
		end
	end)
	
	return function() return valor end
end

-- FUNÇÕES
local getAuto = criarToggle("Auto Attack", 50)
local getEsp = criarToggle("ESP", 110)
local getSpin = criarToggle("Spin Bot", 170)
local getReset = criarToggle("Reset Player", 230)
local getJump = criarToggle("Super Pulo", 290)
local getAutoHit = criarToggle("Auto Hit", 350)
local getAntiHit = criarToggle("Anti Hit", 410) -- Anti Hit
local getSpeedToggle = criarToggle("Speed", 470)
local speedValue = criarSlider("Velocidade", 530, 16, 120, 50)

-- CRÉDITO
local credit = Instance.new("TextLabel", frame)
credit.Size = UDim2.new(1,0,0,20)
credit.Position = UDim2.new(0,0,1,-20)
credit.Text = "Feito Por Zzz.oficial"
credit.Font = Enum.Font.GothamBold
credit.TextColor3 = Color3.fromRGB(150,150,150)
credit.BackgroundTransparency = 1

-- ABRIR / FECHAR
openBtn.MouseButton1Click:Connect(function()
	frame.Visible = not frame.Visible
end)

close.MouseButton1Click:Connect(function()
	frame.Visible = false
end)

-- AUTO ATTACK (Movimento em direção ao inimigo)
RunService.RenderStepped:Connect(function()
	if getAuto() and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then

		local hrp = player.Character.HumanoidRootPart
		local closest, dist = nil, math.huge

		for _,plr in pairs(Players:GetPlayers()) do
			if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
				local d = (plr.Character.HumanoidRootPart.Position - hrp.Position).Magnitude
				if d < dist then
					dist = d
					closest = plr
				end
			end
		end

		if closest then
			local target = closest.Character.HumanoidRootPart.Position
			hrp.Velocity = (target - hrp.Position).Unit * 60
		end
	end
end)

-- AUTO HIT (Bate automaticamente no inimigo)
RunService.RenderStepped:Connect(function()
	if getAutoHit() and player.Character then
		local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
		local hrp = player.Character:FindFirstChild("HumanoidRootPart")
		
		if humanoid and hrp then
			local closest, dist = nil, math.huge
			
			for _,plr in pairs(Players:GetPlayers()) do
				if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
					local targetHrp = plr.Character.HumanoidRootPart
					local d = (targetHrp.Position - hrp.Position).Magnitude
					
					if d < dist and d < 10 then
						dist = d
						closest = plr
					end
				end
			end
			
			if closest and closest.Character then
				local targetHumanoid = closest.Character:FindFirstChildOfClass("Humanoid")
				if targetHumanoid and targetHumanoid.Health > 0 then
					humanoid:MoveTo(closest.Character.HumanoidRootPart.Position)
					
					local tool = player.Character:FindFirstChildOfClass("Tool")
					if tool then
						tool:Activate()
					end
					
					local activeTool = player.Character:FindFirstChildOfClass("Tool")
					if activeTool then
						activeTool:Activate()
					end
				end
			end
		end
	end
end)

-- ANTI HIT (Imunidade a dano)
local originalHealth = nil
local originalMaxHealth = nil

RunService.RenderStepped:Connect(function()
	if getAntiHit() and player.Character then
		local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
		if humanoid then
			-- Salva a saúde original se ainda não salvou
			if originalHealth == nil then
				originalHealth = humanoid.Health
				originalMaxHealth = humanoid.MaxHealth
			end
			
			-- Mantém a saúde no máximo
			if humanoid.Health < originalMaxHealth then
				humanoid.Health = originalMaxHealth
			end
			
			-- Remove efeitos de dano como queimadura, veneno, etc.
			for _, effect in pairs(player.Character:GetChildren()) do
				if effect:IsA("Fire") or effect:IsA("Smoke") or effect:IsA("Sparkles") then
					effect:Destroy()
				end
			end
		end
	else
		-- Reseta quando desativado
		if originalHealth ~= nil and player.Character then
			local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.Health = originalHealth
			end
			originalHealth = nil
			originalMaxHealth = nil
		end
	end
end)

-- Conexão para detectar dano e prevenir (método alternativo)
if player.Character then
	local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid:GetPropertyChangedSignal("Health"):Connect(function()
			if getAntiHit() and humanoid and originalMaxHealth then
				if humanoid.Health < originalMaxHealth then
					humanoid.Health = originalMaxHealth
				end
			end
		end)
	end
end

-- Conexão para quando o personagem renascer
player.CharacterAdded:Connect(function(character)
	task.wait(0.5)
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid:GetPropertyChangedSignal("Health"):Connect(function()
			if getAntiHit() and humanoid then
				local maxHealth = humanoid.MaxHealth
				if humanoid.Health < maxHealth then
					humanoid.Health = maxHealth
				end
			end
		end)
	end
	
	-- Atualiza a referência
	if getAntiHit() then
		originalHealth = nil
		originalMaxHealth = nil
	end
end)

-- SPEED (Velocidade ajustável)
RunService.RenderStepped:Connect(function()
	if player.Character then
		local humanoid = player.Character:FindFirstChildOfClass("Humanoid")
		if humanoid then
			if getSpeedToggle() then
				local speed = speedValue()
				humanoid.WalkSpeed = speed
			else
				if humanoid.WalkSpeed ~= 16 then
					humanoid.WalkSpeed = 16
				end
			end
		end
	end
end)

-- SPIN BOT
RunService.RenderStepped:Connect(function()
	if getSpin() and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
		local hrp = player.Character.HumanoidRootPart
		hrp.CFrame = hrp.CFrame * CFrame.Angles(0, math.rad(25), 0)
	end
end)

-- RESET PLAYER
local lastReset = false

RunService.RenderStepped:Connect(function()
	if getReset() and not lastReset then
		lastReset = true

		if player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
			player.Character:FindFirstChildOfClass("Humanoid").Health = 0
		end

		task.wait(1)
		lastReset = false
	end
end)

-- SUPER JUMP
RunService.RenderStepped:Connect(function()
	if getJump() and player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
		player.Character:FindFirstChildOfClass("Humanoid").JumpPower = 120
	else
		if player.Character and player.Character:FindFirstChildOfClass("Humanoid") then
			player.Character:FindFirstChildOfClass("Humanoid").JumpPower = 50
		end
	end
end)

-- ESP com Aura Vermelha
RunService.RenderStepped:Connect(function()
	if getEsp() then
		for _,plr in pairs(Players:GetPlayers()) do
			if plr ~= player and plr.Character and plr.Character:FindFirstChild("Head") then

				local head = plr.Character.Head
				local esp = head:FindFirstChild("ESP")
				local aura = plr.Character:FindFirstChild("Aura")

				if not esp then
					esp = Instance.new("BillboardGui", head)
					esp.Name = "ESP"
					esp.Size = UDim2.new(0,100,0,40)
					esp.AlwaysOnTop = true

					local txt = Instance.new("TextLabel", esp)
					txt.Size = UDim2.new(1,0,1,0)
					txt.BackgroundTransparency = 1
					txt.TextColor3 = Color3.fromRGB(255,0,0)
					txt.Font = Enum.Font.GothamBold
					txt.TextScaled = true
				end

				local txt = esp:FindFirstChildOfClass("TextLabel")
				if txt and player.Character then
					local d = (head.Position - player.Character.Head.Position).Magnitude
					txt.Text = math.floor(d).."m"
				end
				
				if not aura then
					local highlight = Instance.new("Highlight")
					highlight.Name = "Aura"
					highlight.Parent = plr.Character
					highlight.FillColor = Color3.fromRGB(255,0,0)
					highlight.OutlineColor = Color3.fromRGB(255,0,0)
					highlight.FillTransparency = 0.5
					highlight.OutlineTransparency = 0
					highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
				end
			end
		end
	else
		for _,plr in pairs(Players:GetPlayers()) do
			if plr.Character and plr.Character:FindFirstChild("Head") then
				local esp = plr.Character.Head:FindFirstChild("ESP")
				if esp then esp:Destroy() end
			end
			if plr.Character and plr.Character:FindFirstChild("Aura") then
				plr.Character:FindFirstChild("Aura"):Destroy()
			end
		end
	end
end)
	end
end)
