local Player = game.Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Debris = game:GetService("Debris")
local TweenService = game:GetService("TweenService")

ReplicatedStorage.ThunderBreathingSkill1.OnClientEvent:Connect(function(Player)
	local Character = Player.Character	
	
	local CNTN = script.CNTN:Clone()
	CNTN.Parent = Character.HumanoidRootPart
	local ThunderBreathingSkill1Assets = ReplicatedStorage.ThunderBreathingSkill1Assets:Clone()
	local LightningBoltsfolder = Instance.new("Folder", game.Workspace.Terrain)
	LightningBoltsfolder.Name = "LightningBoltsfolder"
	Debris:AddItem(LightningBoltsfolder, 17)
	ThunderBreathingSkill1Assets.Parent = game.Workspace
	Debris:AddItem(ThunderBreathingSkill1Assets, 15.5)
	ThunderBreathingSkill1Assets.Beam.Attachment0 = ThunderBreathingSkill1Assets.Part1.Attachment1
	ThunderBreathingSkill1Assets.Beam.Attachment1 = ThunderBreathingSkill1Assets.Part2.Attachment2
	local LightningBolt3 = require(ReplicatedStorage.LightningBolt3)
	local LightningBolt2 = require(ReplicatedStorage.LightningBolt2)
	local part1, part2 = ThunderBreathingSkill1Assets.Part1, ThunderBreathingSkill1Assets.Part2
	local a1, a2 = part1.Attachment1, part2.Attachment2


	function CubicBezier(p0, p1, p2, p3, t) --returns pos and tangent vectors
		return p0*(1 - t)^3 + p1*3*t*(1 - t)^2 + p2*3*(1 - t)*t^2 + p3*t^3, (p1 - p0)*3*(1 - t)^2 + 6*(1 - t)*t*(p2 - p1) + (p3 - p2)*3*t^2
	end




	--local NewBolt = LightningBolt.new(a1, a2, workspace.Beam.CurveSize0, workspace.Beam.CurveSize1, 40)
	local LightningSparks3 = require(ReplicatedStorage.LightningBolt3.LightningSparks3)
	local LightningSparks = require(ReplicatedStorage.LightningBolt.LightningSparks)
	local LightningSparks2 = require(ReplicatedStorage.LightningBolt2.LightningSparks2)

	ThunderBreathingSkill1Assets.Part1.Position = Character.HumanoidRootPart.Position + Vector3.new(0,2,0)
	ThunderBreathingSkill1Assets.Part2.Position = Character.HumanoidRootPart.Position + Vector3.new(0,-1,0)
	CNTN.Playing = true
	Debris:AddItem(CNTN, 12.5)
	for i = 1, 20 do
		local ranCF = CFrame.fromAxisAngle((part2.Position - part1.Position).Unit, 0.1*math.random()*math.pi)
		local A1, A2 = {}, {}

		A1.WorldPosition, A1.WorldAxis = a1.WorldPosition, ranCF*a1.WorldAxis
		A2.WorldPosition, A2.WorldAxis = a2.WorldPosition, ranCF*a2.WorldAxis
		local NewBolt = LightningBolt3.new(A1, A2, 20)
		NewBolt.CurveSize0, NewBolt.CurveSize1 = ThunderBreathingSkill1Assets.Beam.CurveSize0, ThunderBreathingSkill1Assets.Beam.CurveSize1
		NewBolt.PulseSpeed = 1
		NewBolt.PulseLength = 0.1
		NewBolt.FadeLength = 0.05
		--NewBolt.MaxRadius = 1
		local Teal = Color3.new(0, 1, 1)
		local Yellow = Color3.new(1, 1, 0)
		NewBolt.Color = ColorSequence.new{
			ColorSequenceKeypoint.new(0, Yellow),
			ColorSequenceKeypoint.new(1, Teal)
		}


		local NewSparks3 = LightningSparks3.new(NewBolt)
		wait(0.25)
	end
	local SFX1 = script.SFX1:Clone()
	local SFX2 = script.SFX2:Clone()
	local SFX3 = script.SFX3:Clone()
	local SFX4 = script.SFX4:Clone()
	SFX1.Parent = Character.HumanoidRootPart
	SFX2.Parent = Character.HumanoidRootPart
	SFX3.Parent = Character.HumanoidRootPart
	SFX4.Parent = Character.HumanoidRootPart
	SFX1.Playing = true
	SFX2.Playing = true
	SFX3.Playing = true
	Debris:AddItem(SFX1, 1.5)
	Debris:AddItem(SFX2, 1)
	Debris:AddItem(SFX3, 2)
	local GroundModule = require(ReplicatedStorage.RockScript)
	GroundModule.Ground(Character.HumanoidRootPart,15,5,20,5)
	
	local ThunderFolder = Instance.new("Folder", game.Workspace)
	ThunderFolder.Name = "ThunderFolder"
	Debris:AddItem(ThunderFolder, 2.5)
	
	local Dash = ReplicatedStorage.ThunderAssets.Dash:Clone()
	Dash.Parent = ThunderFolder
	Dash.CFrame = Character.HumanoidRootPart.CFrame
	ThunderBreathingSkill1Assets.Part1.CFrame = Character.HumanoidRootPart.CFrame

			local tweenInfo = TweenInfo.new(
				0.1, 
				Enum.EasingStyle.Linear,
				Enum.EasingDirection.Out,
				0, 
				false, 
				0 
			)

	local tween = TweenService:Create(Dash, tweenInfo, {Size = Vector3.new(40, 10, 40)})
	tween:Play()
	local Speed = 250
	
	local BodyVelocity = Instance.new("BodyVelocity")
	BodyVelocity.MaxForce = Vector3.new(50000,50000,50000)
	BodyVelocity.Velocity = Character.HumanoidRootPart.CFrame.lookVector * Speed
	BodyVelocity.Parent = Character.HumanoidRootPart
	Debris:AddItem(BodyVelocity, 0.1)
	wait(0.75)
	SFX4.Playing = true
	Debris:AddItem(SFX4, 2.5)
	local tweenInfo2 = TweenInfo.new(
		1, 
		Enum.EasingStyle.Linear,
		Enum.EasingDirection.Out,
		0, 
		false, 
		0 
	)

	local tween2 = TweenService:Create(Dash, tweenInfo2, {Size = Vector3.new(60, 15, 60),Transparency = 1})
	tween2:Play()
	
	local SWAVE = ReplicatedStorage.ThunderAssets.SWAVE:Clone()
	SWAVE.Parent = ThunderFolder
	SWAVE.CFrame = Character.HumanoidRootPart.CFrame * CFrame.new(0,-2,0)
	
	local SWAVEtween1 = TweenService:Create(SWAVE, tweenInfo, {Size = Vector3.new(40, 2, 40),Transparency = 0})
	local SWAVEtween2 = TweenService:Create(SWAVE, tweenInfo2, {Size = Vector3.new(60, 3, 60),Transparency = 1})
	SWAVEtween1:Play()
			
	local HitBox = Instance.new("Part", game.Workspace)
	local function dmg()
		local AlrDamagedList = {}
		HitBox.Touched:Connect(function(hit)
			if hit.Parent:FindFirstChild("Humanoid") ~= nil and hit.Parent then
				local EnemyCharacter = hit.Parent
				if not hit:IsDescendantOf(Player.Character) and EnemyCharacter.Humanoid:GetState() ~= Enum.HumanoidStateType.Dead and not AlrDamagedList[EnemyCharacter] then
					hit.Parent.Humanoid:TakeDamage(18)
					AlrDamagedList[EnemyCharacter] = true
				end			
			end
		end)
	end
			HitBox.Name = "HitBox"
			HitBox.Transparency = 1
			HitBox.Anchored = true
			HitBox.CanCollide = false
			HitBox.Size = Vector3.new(20, 40, 125)
	HitBox.CFrame = Character.HumanoidRootPart.CFrame * CFrame.new(0,0,60)
	
	dmg()
	
	ThunderBreathingSkill1Assets.Part2.CFrame = Character.HumanoidRootPart.CFrame
	
	for i = 1, 200 do
		local ranCF = CFrame.fromAxisAngle((part2.Position - part1.Position).Unit, 0.1*math.random()*math.pi)
		local A1, A2 = {}, {}

		A1.WorldPosition, A1.WorldAxis = a1.WorldPosition, ranCF*a1.WorldAxis
		A2.WorldPosition, A2.WorldAxis = a2.WorldPosition, ranCF*a2.WorldAxis
		local NewBolt2 = LightningBolt3.new(A1, A2, 20)
		NewBolt2.CurveSize0, NewBolt2.CurveSize1 = ThunderBreathingSkill1Assets.Beam.CurveSize0, ThunderBreathingSkill1Assets.Beam.CurveSize1
		NewBolt2.PulseSpeed = 40
		NewBolt2.PulseLength = 10
		NewBolt2.FadeLength = 5
		--NewBolt2.MaxRadius = 1
		local Teal = Color3.new(0, 1, 1)
		local Yellow = Color3.new(1, 1, 0)
		NewBolt2.Color = ColorSequence.new{
			ColorSequenceKeypoint.new(0, Yellow),
			ColorSequenceKeypoint.new(1, Teal)
		}


		local NewSparks3 = LightningSparks3.new(NewBolt2)
		wait(0.01)
	end
	
	wait(1.5)
	Character.Humanoid.WalkSpeed = 16
	Character.Humanoid.JumpHeight = 7.2
	Character.Humanoid.AutoRotate = true
	Character.CanDoAnything.Value = true
	Character.CanDoSkill.Value = true
	
					
end)
