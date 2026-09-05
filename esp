local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

local SETTINGS = {
	Enabled = true,

	ShowSkeleton = true,
	ShowTracker = true,

	ShowName = true,
	ShowHealth = true,
	ShowDistance = true,

	MinScale = 0.18,
	MaxScale = 1.65,

	ReferenceCharacterHeight = 120,

	BaseTextSize = 15,

	SkeletonThickness = 2,

	TrackerThickness = 1.5,

	TrackerBottomOffset = 90,

	TrackerScreenMargin = 15,
}

local ScreenGui = Instance.new("ScreenGui")

ScreenGui.Name = "PlayerESP"
ScreenGui.IgnoreGuiInset = true
ScreenGui.ResetOnSpawn = false
ScreenGui.DisplayOrder = 999999
ScreenGui.Parent = PlayerGui

local ESPObjects = {}

local function CreateCorner(parent, radius)

	local corner = Instance.new("UICorner")

	corner.CornerRadius =
		UDim.new(
			0,
			radius
		)

	corner.Parent = parent

	return corner

end

local function CreateLine(
	parent,
	name,
	transparency
)

	local line =
		Instance.new("Frame")

	line.Name =
		name or "Line"

	line.AnchorPoint =
		Vector2.new(
			0.5,
			0.5
		)

	line.BackgroundColor3 =
		Color3.fromRGB(
			255,
			255,
			255
		)

	line.BackgroundTransparency =
		transparency or 0

	line.BorderSizePixel = 0

	line.Visible = false

	line.ZIndex = 10

	line.Parent = parent

	return line

end

local function DrawLine(
	line,
	pointA,
	pointB,
	thickness
)

	local delta =
		pointB - pointA

	local length =
		delta.Magnitude

	if length <= 0.01 then

		line.Visible = false

		return

	end

	local middle =
		(pointA + pointB) / 2

	line.Position =
		UDim2.fromOffset(
			middle.X,
			middle.Y
		)

	line.Size =
		UDim2.fromOffset(
			length,
			thickness
		)

	line.Rotation =
		math.deg(
			math.atan2(
				delta.Y,
				delta.X
			)
		)

	line.Visible = true

end

local Menu =
	Instance.new("Frame")

Menu.Name = "ESPMenu"

Menu.Size =
	UDim2.fromOffset(
		132,
		116
	)

Menu.Position =
	UDim2.fromOffset(
		18,
		180
	)

Menu.BackgroundColor3 =
	Color3.fromRGB(
		22,
		22,
		27
	)

Menu.BorderSizePixel = 0

Menu.Active = true

Menu.ZIndex = 10000

Menu.Parent =
	ScreenGui

CreateCorner(
	Menu,
	10
)

local MenuStroke =
	Instance.new("UIStroke")

MenuStroke.Color =
	Color3.fromRGB(
		60,
		60,
		70
	)

MenuStroke.Thickness = 1

MenuStroke.Parent =
	Menu

local Header =
	Instance.new("TextLabel")

Header.Name = "Header"

Header.Size =
	UDim2.new(
		1,
		0,
		0,
		28
	)

Header.BackgroundTransparency = 1

Header.Text = "ESP"

Header.TextColor3 =
	Color3.fromRGB(
		255,
		255,
		255
	)

Header.Font =
	Enum.Font.GothamBold

Header.TextSize = 13

Header.TextXAlignment =
	Enum.TextXAlignment.Left

Header.Position =
	UDim2.fromOffset(
		10,
		0
	)

Header.ZIndex = 10001

Header.Active = true

Header.Parent =
	Menu

local Divider =
	Instance.new("Frame")

Divider.Size =
	UDim2.new(
		1,
		-16,
		0,
		1
	)

Divider.Position =
	UDim2.fromOffset(
		8,
		27
	)

Divider.BackgroundColor3 =
	Color3.fromRGB(
		50,
		50,
		58
	)

Divider.BorderSizePixel = 0

Divider.ZIndex = 10001

Divider.Parent =
	Menu

local function CreateToggleRow(
	parent,
	text,
	yPosition,
	defaultState
)

	local Row =
		Instance.new("TextButton")

	Row.Name =
		text .. "Row"

	Row.Size =
		UDim2.new(
			1,
			-12,
			0,
			27
		)

	Row.Position =
		UDim2.fromOffset(
			6,
			yPosition
		)

	Row.BackgroundTransparency = 1

	Row.Text = ""

	Row.AutoButtonColor = false

	Row.ZIndex = 10001

	Row.Parent =
		parent

	local Label =
		Instance.new("TextLabel")

	Label.Size =
		UDim2.new(
			1,
			-44,
			1,
			0
		)

	Label.BackgroundTransparency = 1

	Label.Text =
		text

	Label.TextColor3 =
		Color3.fromRGB(
			225,
			225,
			230
		)

	Label.Font =
		Enum.Font.GothamMedium

	Label.TextSize = 11

	Label.TextXAlignment =
		Enum.TextXAlignment.Left

	Label.ZIndex = 10002

	Label.Parent =
		Row

	local Switch =
		Instance.new("Frame")

	Switch.Size =
		UDim2.fromOffset(
			32,
			18
		)

	Switch.Position =
		UDim2.new(
			1,
			-34,
			0.5,
			-9
		)

	Switch.BorderSizePixel = 0

	Switch.ZIndex = 10002

	Switch.Parent =
		Row

	CreateCorner(
		Switch,
		9
	)

	local Circle =
		Instance.new("Frame")

	Circle.Size =
		UDim2.fromOffset(
			14,
			14
		)

	Circle.BorderSizePixel = 0

	Circle.BackgroundColor3 =
		Color3.fromRGB(
			255,
			255,
			255
		)

	Circle.ZIndex = 10003

	Circle.Parent =
		Switch

	CreateCorner(
		Circle,
		7
	)

	local state =
		defaultState

	local function UpdateVisual()

		if state then

			Switch.BackgroundColor3 =
				Color3.fromRGB(
					60,
					190,
					90
				)

			Circle.Position =
				UDim2.new(
					1,
					-16,
					0.5,
					-7
				)

			Label.TextColor3 =
				Color3.fromRGB(
					240,
					240,
					245
				)

		else

			Switch.BackgroundColor3 =
				Color3.fromRGB(
					67,
					67,
					75
				)

			Circle.Position =
				UDim2.new(
					0,
					2,
					0.5,
					-7
				)

			Label.TextColor3 =
				Color3.fromRGB(
					150,
					150,
					158
				)

		end

	end

	UpdateVisual()

	return {

		Row = Row,

		GetState =
			function()

				return state

			end,

		SetState =
			function(value)

				state = value

				UpdateVisual()

			end
	}

end

local ESPToggle =
	CreateToggleRow(
		Menu,
		"ESP",
		31,
		SETTINGS.Enabled
	)

local TrackerToggle =
	CreateToggleRow(
		Menu,
		"Tracker",
		58,
		SETTINGS.ShowTracker
	)

local SkeletonToggle =
	CreateToggleRow(
		Menu,
		"Skeleton",
		85,
		SETTINGS.ShowSkeleton
	)

local function HideESP(data)

	if data.Info then

		data.Info.Visible = false

	end

	if data.Tracker then

		data.Tracker.Visible = false

	end

	for _, line in ipairs(
		data.Lines
	) do

		line.Visible = false

	end

end

ESPToggle.Row.MouseButton1Click:Connect(
	function()

		SETTINGS.Enabled =
			not SETTINGS.Enabled

		ESPToggle.SetState(
			SETTINGS.Enabled
		)

		if not SETTINGS.Enabled then

			for _, data in pairs(
				ESPObjects
			) do

				HideESP(data)

			end

		end

	end
)

TrackerToggle.Row.MouseButton1Click:Connect(
	function()

		SETTINGS.ShowTracker =
			not SETTINGS.ShowTracker

		TrackerToggle.SetState(
			SETTINGS.ShowTracker
		)

		if not SETTINGS.ShowTracker then

			for _, data in pairs(
				ESPObjects
			) do

				if data.Tracker then

					data.Tracker.Visible = false

				end

			end

		end

	end
)

SkeletonToggle.Row.MouseButton1Click:Connect(
	function()

		SETTINGS.ShowSkeleton =
			not SETTINGS.ShowSkeleton

		SkeletonToggle.SetState(
			SETTINGS.ShowSkeleton
		)

		if not SETTINGS.ShowSkeleton then

			for _, data in pairs(
				ESPObjects
			) do

				for _, line in ipairs(
					data.Lines
				) do

					line.Visible = false

				end

			end

		end

	end
)

local Dragging = false
local DragStart = nil
local StartPosition = nil

Header.InputBegan:Connect(
	function(input)

		if input.UserInputType ==
			Enum.UserInputType.MouseButton1
			or
			input.UserInputType ==
			Enum.UserInputType.Touch then

			Dragging = true

			DragStart =
				input.Position

			StartPosition =
				Menu.Position

		end

	end
)

UserInputService.InputChanged:Connect(
	function(input)

		if not Dragging then
			return
		end

		if input.UserInputType ~=
			Enum.UserInputType.MouseMovement
			and
			input.UserInputType ~=
			Enum.UserInputType.Touch then

			return

		end

		local camera =
			workspace.CurrentCamera

		if not camera then
			return
		end

		local delta =
			input.Position
			-
			DragStart

		local viewport =
			camera.ViewportSize

		local x =
			StartPosition.X.Offset
			+
			delta.X

		local y =
			StartPosition.Y.Offset
			+
			delta.Y

		x =
			math.clamp(
				x,
				0,
				viewport.X
				-
				Menu.AbsoluteSize.X
			)

		y =
			math.clamp(
				y,
				0,
				viewport.Y
				-
				Menu.AbsoluteSize.Y
			)

		Menu.Position =
			UDim2.fromOffset(
				x,
				y
			)

	end
)

UserInputService.InputEnded:Connect(
	function(input)

		if input.UserInputType ==
			Enum.UserInputType.MouseButton1
			or
			input.UserInputType ==
			Enum.UserInputType.Touch then

			Dragging = false

		end

	end
)

local R15Connections = {

	{"Head", "UpperTorso"},

	{"UpperTorso", "LowerTorso"},

	{"UpperTorso", "LeftUpperArm"},
	{"LeftUpperArm", "LeftLowerArm"},
	{"LeftLowerArm", "LeftHand"},

	{"UpperTorso", "RightUpperArm"},
	{"RightUpperArm", "RightLowerArm"},
	{"RightLowerArm", "RightHand"},

	{"LowerTorso", "LeftUpperLeg"},
	{"LeftUpperLeg", "LeftLowerLeg"},
	{"LeftLowerLeg", "LeftFoot"},

	{"LowerTorso", "RightUpperLeg"},
	{"RightUpperLeg", "RightLowerLeg"},
	{"RightLowerLeg", "RightFoot"},
}

local R6Connections = {

	{"Head", "Torso"},

	{"Torso", "Left Arm"},
	{"Torso", "Right Arm"},

	{"Torso", "Left Leg"},
	{"Torso", "Right Leg"},
}

local function GetVisualScale(
	character,
	camera
)

	local Head =
		character:FindFirstChild(
			"Head"
		)

	local Root =
		character:FindFirstChild(
			"HumanoidRootPart"
		)

	if not Head
		or
		not Root then

		return SETTINGS.MinScale

	end

	local Top =
		Head.Position
		+
		Vector3.new(
			0,
			1,
			0
		)

	local Bottom =
		Root.Position
		-
		Vector3.new(
			0,
			3,
			0
		)

	local TopScreen =
		camera:WorldToViewportPoint(
			Top
		)

	local BottomScreen =
		camera:WorldToViewportPoint(
			Bottom
		)

	if TopScreen.Z <= 0
		or
		BottomScreen.Z <= 0 then

		return SETTINGS.MinScale

	end

	local CharacterHeight =
		math.abs(
			BottomScreen.Y
			-
			TopScreen.Y
		)

	local scale =
		CharacterHeight
		/
		SETTINGS.ReferenceCharacterHeight

	return math.clamp(
		scale,
		SETTINGS.MinScale,
		SETTINGS.MaxScale
	)

end

local function GetHealthColor(percent)

	if percent >= 0.6 then

		return Color3.fromRGB(
			60,
			255,
			90
		)

	elseif percent >= 0.3 then

		return Color3.fromRGB(
			255,
			195,
			45
		)

	else

		return Color3.fromRGB(
			255,
			55,
			60
		)

	end

end

local function GetTrackerTarget(
	camera,
	worldPosition
)

	local viewport =
		camera.ViewportSize

	local projected =
		camera:WorldToViewportPoint(
			worldPosition
		)

	local center =
		Vector2.new(
			viewport.X / 2,
			viewport.Y / 2
		)

	local target =
		Vector2.new(
			projected.X,
			projected.Y
		)

	local margin =
		SETTINGS.TrackerScreenMargin

	if projected.Z <= 0 then

		local direction =
			target - center

		if direction.Magnitude <= 0.01 then

			direction =
				Vector2.new(
					0,
					-1
				)

		else

			direction =
				direction.Unit

		end

		direction =
			-direction

		target =
			center
			+
			direction
			*
			math.max(
				viewport.X,
				viewport.Y
			)

	end

	target =
		Vector2.new(

			math.clamp(
				target.X,
				margin,
				viewport.X - margin
			),

			math.clamp(
				target.Y,
				margin,
				viewport.Y - margin
			)

		)

	return target

end

local function CreateESP(player)

	if player == LocalPlayer then
		return
	end

	if ESPObjects[player] then
		return
	end

	local Container =
		Instance.new("Folder")

	Container.Name =
		"ESP_" .. player.Name

	Container.Parent =
		ScreenGui

	local SkeletonFolder =
		Instance.new("Folder")

	SkeletonFolder.Name =
		"Skeleton"

	SkeletonFolder.Parent =
		Container

	local Lines = {}

	for i = 1, 20 do

		Lines[i] =
			CreateLine(
				SkeletonFolder,
				"Bone",
				0
			)

	end

	local Tracker =
		CreateLine(
			Container,
			"Tracker",
			0.35
		)

	Tracker.ZIndex = 5

	local Info =
		Instance.new("Frame")

	Info.Size =
		UDim2.fromOffset(
			240,
			65
		)

	Info.AnchorPoint =
		Vector2.new(
			0.5,
			1
		)

	Info.BackgroundTransparency = 1

	Info.Visible = false

	Info.Parent =
		Container

	local Scale =
		Instance.new("UIScale")

	Scale.Scale = 1

	Scale.Parent =
		Info

	local NameLabel =
		Instance.new("TextLabel")

	NameLabel.Size =
		UDim2.new(
			1,
			0,
			0,
			22
		)

	NameLabel.BackgroundTransparency = 1

	NameLabel.TextColor3 =
		Color3.fromRGB(
			255,
			255,
			255
		)

	NameLabel.TextStrokeColor3 =
		Color3.fromRGB(
			0,
			0,
			0
		)

	NameLabel.TextStrokeTransparency = 0

	NameLabel.Font =
		Enum.Font.GothamBold

	NameLabel.TextSize =
		SETTINGS.BaseTextSize

	NameLabel.Parent =
		Info

	local DistanceLabel =
		Instance.new("TextLabel")

	DistanceLabel.Position =
		UDim2.fromOffset(
			0,
			21
		)

	DistanceLabel.Size =
		UDim2.new(
			1,
			0,
			0,
			17
		)

	DistanceLabel.BackgroundTransparency = 1

	DistanceLabel.TextColor3 =
		Color3.fromRGB(
			220,
			220,
			220
		)

	DistanceLabel.TextStrokeColor3 =
		Color3.fromRGB(
			0,
			0,
			0
		)

	DistanceLabel.TextStrokeTransparency = 0

	DistanceLabel.Font =
		Enum.Font.Gotham

	DistanceLabel.TextSize = 12

	DistanceLabel.Parent =
		Info

	local HealthText =
		Instance.new("TextLabel")

	HealthText.Position =
		UDim2.fromOffset(
			0,
			40
		)

	HealthText.Size =
		UDim2.fromOffset(
			28,
			15
		)

	HealthText.BackgroundTransparency = 1

	HealthText.TextColor3 =
		Color3.fromRGB(
			255,
			255,
			255
		)

	HealthText.TextStrokeColor3 =
		Color3.fromRGB(
			0,
			0,
			0
		)

	HealthText.TextStrokeTransparency = 0

	HealthText.Font =
		Enum.Font.GothamBold

	HealthText.TextSize = 10

	HealthText.Parent =
		Info

	local HealthBackground =
		Instance.new("Frame")

	HealthBackground.Position =
		UDim2.fromOffset(
			30,
			43
		)

	HealthBackground.Size =
		UDim2.fromOffset(
			180,
			8
		)

	HealthBackground.BackgroundColor3 =
		Color3.fromRGB(
			25,
			25,
			30
		)

	HealthBackground.BorderSizePixel = 0

	HealthBackground.ClipsDescendants = true

	HealthBackground.Parent =
		Info

	CreateCorner(
		HealthBackground,
		4
	)

	local HealthFill =
		Instance.new("Frame")

	HealthFill.Size =
		UDim2.fromScale(
			1,
			1
		)

	HealthFill.BackgroundColor3 =
		Color3.fromRGB(
			60,
			255,
			90
		)

	HealthFill.BorderSizePixel = 0

	HealthFill.Parent =
		HealthBackground

	CreateCorner(
		HealthFill,
		4
	)

	ESPObjects[player] = {

		Container = Container,

		Lines = Lines,

		Tracker = Tracker,

		Info = Info,

		Scale = Scale,

		Name = NameLabel,

		Distance = DistanceLabel,

		HealthText = HealthText,

		HealthBackground =
			HealthBackground,

		HealthFill =
			HealthFill,
	}

end

local function RemoveESP(player)

	local data =
		ESPObjects[player]

	if not data then
		return
	end

	if data.Container then

		data.Container:Destroy()

	end

	ESPObjects[player] = nil

end

local function UpdateESP(
	player,
	data
)

	if not SETTINGS.Enabled then

		HideESP(data)

		return

	end

	local Character =
		player.Character

	if not Character then

		HideESP(data)

		return

	end

	local Humanoid =
		Character:FindFirstChildOfClass(
			"Humanoid"
		)

	local Root =
		Character:FindFirstChild(
			"HumanoidRootPart"
		)

	local Head =
		Character:FindFirstChild(
			"Head"
		)

	if not Humanoid
		or
		not Root
		or
		not Head then

		HideESP(data)

		return

	end

	local MyCharacter =
		LocalPlayer.Character

	if not MyCharacter then
		return
	end

	local MyRoot =
		MyCharacter:FindFirstChild(
			"HumanoidRootPart"
		)

	if not MyRoot then
		return
	end

	local Camera =
		workspace.CurrentCamera

	if not Camera then
		return
	end

	local Viewport =
		Camera.ViewportSize

	local Distance =
		(
			MyRoot.Position
			-
			Root.Position
		).Magnitude

	local scale =
		GetVisualScale(
			Character,
			Camera
		)

	data.Scale.Scale =
		scale

	if SETTINGS.ShowTracker then

		local TrackerStart =
			Vector2.new(

				Viewport.X / 2,

				Viewport.Y
				-
				SETTINGS.TrackerBottomOffset
			)

		local TrackerEnd =
			GetTrackerTarget(
				Camera,
				Root.Position
			)

		DrawLine(

			data.Tracker,

			TrackerStart,

			TrackerEnd,

			SETTINGS.TrackerThickness
		)

	else

		data.Tracker.Visible =
			false

	end

	local HeadScreen,
	HeadVisible =
		Camera:WorldToViewportPoint(

			Head.Position
			+
			Vector3.new(
				0,
				1.2,
				0
			)
		)

	if HeadScreen.Z > 0
		and
		HeadVisible then

		data.Info.Position =
			UDim2.fromOffset(
				HeadScreen.X,
				HeadScreen.Y
			)

		data.Info.Visible = true

	else

		data.Info.Visible = false

	end

	if SETTINGS.ShowName then

		data.Name.Visible = true

		data.Name.Text =
			player.DisplayName
			..
			" (@"
			..
			player.Name
			..
			")"

	else

		data.Name.Visible = false

	end

	if SETTINGS.ShowDistance then

		data.Distance.Visible = true

		data.Distance.Text =
			tostring(
				math.floor(
					Distance + 0.5
				)
			)
			..
			" studs"

	else

		data.Distance.Visible = false

	end

	local HealthPercent = 0

	if Humanoid.MaxHealth > 0 then

		HealthPercent =
			math.clamp(

				Humanoid.Health
				/
				Humanoid.MaxHealth,

				0,
				1
			)

	end

	local Health100 =
		math.floor(
			HealthPercent
			*
			100
			+
			0.5
		)

	if SETTINGS.ShowHealth then

		data.HealthText.Visible =
			true

		data.HealthBackground.Visible =
			true

		data.HealthText.Text =
			tostring(
				Health100
			)

		data.HealthFill.Size =
			UDim2.fromScale(
				HealthPercent,
				1
			)

		data.HealthFill.BackgroundColor3 =
			GetHealthColor(
				HealthPercent
			)

	else

		data.HealthText.Visible =
			false

		data.HealthBackground.Visible =
			false

	end

	for _, line in ipairs(
		data.Lines
	) do

		line.Visible = false

	end

	if not SETTINGS.ShowSkeleton then
		return
	end

	local Connections

	if Humanoid.RigType ==
		Enum.HumanoidRigType.R15 then

		Connections =
			R15Connections

	else

		Connections =
			R6Connections

	end

	local LineIndex = 1

	for _, connection in ipairs(
		Connections
	) do

		local PartA =
			Character:FindFirstChild(
				connection[1]
			)

		local PartB =
			Character:FindFirstChild(
				connection[2]
			)

		if PartA
			and
			PartB
			and
			PartA:IsA("BasePart")
			and
			PartB:IsA("BasePart") then

			local ScreenA =
				Camera:WorldToViewportPoint(
					PartA.Position
				)

			local ScreenB =
				Camera:WorldToViewportPoint(
					PartB.Position
				)

			if ScreenA.Z > 0
				and
				ScreenB.Z > 0 then

				local Line =
					data.Lines[
						LineIndex
					]

				if Line then

					DrawLine(

						Line,

						Vector2.new(
							ScreenA.X,
							ScreenA.Y
						),

						Vector2.new(
							ScreenB.X,
							ScreenB.Y
						),

						SETTINGS.SkeletonThickness
					)

					LineIndex += 1

				end

			end

		end

	end

end

for _, Player in ipairs(
	Players:GetPlayers()
) do

	CreateESP(Player)

end

Players.PlayerAdded:Connect(
	function(Player)

		CreateESP(Player)

	end
)

Players.PlayerRemoving:Connect(
	function(Player)

		RemoveESP(Player)

	end
)

RunService.RenderStepped:Connect(
	function()

		for Player, Data in pairs(
			ESPObjects
		) do

			if Player.Parent ==
				Players then

				UpdateESP(
					Player,
					Data
				)

			else

				RemoveESP(
					Player
				)

			end

		end

	end
)
