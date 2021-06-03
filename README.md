local frm = script.Parent
local uis = game:GetService("UserInputService")
local debounce = false
local timesPressed = 1 -- 1 = opt1, 2 = opt, etc

function visible(int, o1, o2, o3, o4, bool1, bool2, bool3, bool4)
	if timesPressed == int then
		o1.Visible = bool1
		o2.Visible = bool2
		o3.Visible = bool3
		o4.Visible = bool4
	end
end

local opt1 = frm.option1
local opt2 = frm.option2
local opt3 = frm.option3
local opt4 = frm.option4

uis.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.Keyboard then
		if input.KeyCode == Enum.KeyCode.E then
			if not debounce then
				debounce = true
				frm.Rotation += 45
				wait()
				frm.Rotation += 45
				
				print("pressed e")
				
				if timesPressed >= 4 then
					timesPressed = 1
				else
					timesPressed += 1
				end
				
				wait(0.05)
				debounce = false
			end
		end
	end
end)

game:GetService("RunService").Heartbeat:Connect(function()
	if timesPressed == 1 then -- set opt1 visible
		visible(1, opt1, opt2, opt3, opt4, true, false, false, false)
		wait()
	end
	if timesPressed == 2 then -- set opt2 visible
		visible(2, opt1, opt2, opt3, opt4, false, true, false, false)
		wait()
	end
	if timesPressed == 3 then -- set opt3 visible
		visible(3, opt1, opt2, opt3, opt4, false, false, true, false)
		wait()
	end
	if timesPressed == 4 then -- set opt4 visible
		visible(4, opt1, opt2, opt3, opt4, false, false, false, true)
		wait()
	end
end)
