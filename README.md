# Deathnote-Escaperoom-Roblox
## Concept:
Developing a deathnote themed escape room, using multiple puzzles, an in game working computer, and brain busting obstacles to grab the deathnote. Based off a popluar anime,
you are a FBI agent. You enter into Light Yagami's room in hopes of finding the death note.
Right as you enter, Yagami's security system locks the door behind you, leaving you no other option but to find an alternate escape. You have limited time before Yagami comes back home, and he is not happy you're here.
![Deathnote](https://m.media-amazon.com/images/M/MV5BNjRiNmNjMmMtN2U2Yi00ODgxLTk3OTMtMmI1MTI1NjYyZTEzXkEyXkFqcGdeQXVyNjAwNDUxODI@._V1_FMjpg_UX1000_.jpg)
--

## Motivation:
We had this idea of making a Roblox game for experience and projects to put on our plate. Maybe even some cash flow if we get popular. We were planning to make it in Roblox because our years were spent playing Roblox games. We had this planned for a while but never started due to lack of motivation and procrastination. When this assignment was dropped on us we took this as an opportunity to start our very delayed roblox game. This Idea was based on an escape room us three have done in the past about Deathnote. I hope this game turns out as well as we think 👍.
--

## Rough Drafts With Steps and Sources:
[Rough Draft](https://docs.google.com/document/d/1G9Vt_d7KeXPU3AQl7L605vaxcdaqV_0QCVF4iuRkt_o/edit?usp=sharing)

[Link to figma Design](https://www.figma.com/design/yEUEFZYZMyscHEr3VQTPkr/Death-Note-Escape-Room?node-id=0-1&t=Yo9s3PlkmBTVaM8v-1)

[Playlist full of tutorials](https://www.youtube.com/watch?v=BkYwRdCukZA&list=PLhieaQmOk7nIfMZ1UmvKGPrwuwQVwAvFa&ab_channel=TheDevKing)

[Light Yagami's Room](https://www.youtube.com/watch?v=Hhdvph9sH1M&ab_channel=onuryasemin)
--

### THE DATABASE IS ALREADY INCORPORATED WITHIN ROBLOX. We used the pre made one.

--

# Somewhat of the Pseudocode
## Drawers
- TweenService (Built in function to animate with code)
- Call object
- name position
- info of what it does
- goal of the location
- if clicked then
    - play animation

## Keypad
- call each object
- TweenService
- check if button sequence is correct by pressing on number
- if correct then play animation on bookshelf

## Computer
- name each frame
- if interacted then make gui visible and interactable
- when pressed certain location then loads different pages in the frame

--
# Codes
## Drawer code
```
local TweenService = game:GetService("TweenService")
local FrontDrawer1 = script.Parent
local FirstDrawer = script.Parent.Parent
local FirstDrawerX = FirstDrawer.Position.X
local FirstDrawerY = FirstDrawer.Position.Y
local FirstDrawerZ = FirstDrawer.Position.Z
	
local Deathnote = workspace.DeathNote
local DeathnoteX = Deathnote.Position.X
local DeathnoteY = Deathnote.Position.Y
local DeathnoteZ = Deathnote.Position.Z
local Visibility = true

local info = TweenInfo.new(0.6, Enum.EasingStyle.Linear, Enum.EasingDirection.Out, 0, false, 0)
local goal = {Position = Vector3.new(FirstDrawerX + 2.75, FirstDrawerY, FirstDrawerZ)}
local goal2 = {Position = Vector3.new(FirstDrawerX, FirstDrawerY, FirstDrawerZ)}
local goal3 = {Position = Vector3.new(DeathnoteX + 2.75, DeathnoteY, DeathnoteZ)}
local goal4 = {Position = Vector3.new(DeathnoteX, DeathnoteY, DeathnoteZ)}

local tween = TweenService:Create(FirstDrawer, info, goal)
local tween2 = TweenService:Create(FirstDrawer, info, goal2)
local tween3 = TweenService:Create(Deathnote, info, goal3)
local tween4 = TweenService:Create(Deathnote, info, goal4)

local	pressed = false
local	open = false

	FrontDrawer1.MouseClick:Connect(function()	
		print (Visibility)
		if Deathnote.Position.Y < DeathnoteY then
			Visibility = false
		end
		if open == false then
			tween:Play()
			if Visibility == true then
				tween3:Play()
			end
			open = true
		else 
			tween2:Play()
			if Visibility == true then
				tween4:Play()
			end
			open = false
		end	
	end)
```

## KeyPad Code
```
local Button0 = script.Parent.Button0
local Button1 = workspace.KeypadMain.Button1
local Button2 = script.Parent.Button2
local Button3 = script.Parent.Button3
local Button4 = script.Parent.Button4
local Button5 = script.Parent.Button5
local Button6 = script.Parent.Button6
local Button7 = script.Parent.Button7
local Button8 = script.Parent.Button8
local Button9 = script.Parent.Button9
local GreenButton = script.Parent.GreenButton
local RedButton = script.Parent.RedButton
local Display = workspace.KeypadMain.ScreenDisplay.SurfaceGui.TextLabel.Text
local FirstNumber = 0
local SecondNumber = 0
local ThirdNumber = 0 
local FourthNumber = 0
local Input = ""
local RandomNumber = math.random(1000,9999)
local Code = ""
local Code = Code .. RandomNumber
local correct = false 

local TweenService = game:GetService("TweenService")
local Bookshelf = workspace.MovingBookshelf1
local BookshelfX = Bookshelf.Position.X
local BookshelfY = Bookshelf.Position.Y
local BookshelfZ = Bookshelf.Position.Z
local info = TweenInfo.new(1.25, Enum.EasingStyle.Linear, Enum.EasingDirection.Out, 0, false, 0)
local info2 = TweenInfo.new(1, Enum.EasingStyle.Linear, Enum.EasingDirection.Out, 0, false, 0)
local goal = {Position = Vector3.new(BookshelfX, BookshelfY, BookshelfZ - 4.5)}
local goal2 = {Position = Vector3.new(goal.Position.x - 8.4, goal.Position.Y, goal.Position.Z)}
local tween = TweenService:Create(Bookshelf, info, goal)
local tween2 = TweenService:Create(Bookshelf, info2, goal2)

 local function Display()
		workspace.KeypadMain.ScreenDisplay.SurfaceGui.TextLabel.Text = Input
 end
 
if correct == false then
 
	Button0.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 0
			Display()
			print('pressed')
		end 
	end)
	Button1.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 1
			Display()
		end 
	end)
	Button2.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 2
			Display()
			print('pressed')
		end 
	end)
	Button3.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 3
			Display()
			print('pressed')
		end 
	end)
	Button4.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 4
			Display()
		end 
	end)
	Button5.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 5
			Display()
		end 
	end)
	Button6.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 6
			Display()
		end 
	end)

	Button7.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 7
			Display()
		end 
	end)
	Button8.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 8
			Display()
		end 
	end)
	Button9.ClickDetector.MouseClick:Connect(function()
		if string.len(Input) < 4 then
			Input = Input .. 9
			Display()
		end 
	end)
	RedButton.ClickDetector.MouseClick:Connect(function()
		workspace.KeypadMain.ScreenDisplay.BrickColor = BrickColor.Red()
		Input = ""
		Display()
		wait(0.5)
		workspace.KeypadMain.ScreenDisplay.BrickColor = BrickColor.Black()
	end)
	GreenButton.ClickDetector.MouseClick:Connect(function()
		print(Code)
		if Input == Code then
			correct = true
			Input = ""
			Display()
			workspace.KeypadMain.ScreenDisplay.BrickColor = BrickColor.Green()
			print(correct)
			tween:Play()
			wait(1.25)
			tween2:Play()
			print('correct')
		end
		workspace.KeypadMain.ScreenDisplay.BrickColor = BrickColor.Red()
		Input = ""
		Display()
		wait(0.5)
		workspace.KeypadMain.ScreenDisplay.BrickColor = BrickColor.Black()
	end)

end
```

## Computer Code (Working Progress)
```
local function updateCamera()
	local character = player.Character
	if character then
		local root = character:FindFirstChild("HumanoidRootPart")
		if root then
			local rootPosition = root.Position + Vector3.new(0, HEIGHT_OFFSET, 0)
			local cameraPosition = rootPosition + Vector3.new(CAMERA_DEPTH, CAMERA_DEPTH, CAMERA_DEPTH)
			camera.CFrame = CFrame.lookAt(cameraPosition, rootPosition)
		end
	end
end

RunService:BindToRenderStep("IsometricCamera", Enum.RenderPriority.Camera.Value + 1, updateCamera)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local camera = workspace.CurrentCamera

local CAMERA_DEPTH = 64
local HEIGHT_OFFSET = 2

camera.FieldOfView = 20

local function updateCamera()
```

## Flashlight Code
```
local anim = script.Parent:WaitForChild("Humanoid"):LoadAnimation(script.Parent.FlashLight)


script.VisualizeFlashlight.OnServerEvent:Connect(function()
	game.Lighting.Handle:Clone().Parent = script.Parent
	script.Parent:WaitForChild("Handle").Sound:Play()
	local weld = game.Lighting.Weld:Clone()
	weld.Parent = script.Parent
	weld.Part0 = script.Parent.RightHand
	weld.Part1 = script.Parent:WaitForChild("Handle")
	anim:Play()
	script.DisableFpsLight:FireClient(game.Players:GetPlayerFromCharacter(script.Parent))
end)

script.UnVisualizeFlashlight.OnServerEvent:Connect(function()
	script.Parent:WaitForChild("Weld"):Destroy()
	anim:Stop()
	script.Parent:WaitForChild("Handle"):Destroy()
end)
```
