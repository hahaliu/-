# -
--[[
游侠自动刷Boss lua脚本
比例为4:3倍数的屏幕可以用，需要修改物品标签显示为0（想改其他键就同步修改脚本里的键）
关于定同时开箱子和点篝火的点位：先打死一次boss开篝火点位那里出现个点，点一下走过去后再点箱子左边的边缘（边缘能出现开箱子的提示的地方），取消开箱子，鼠标前进侧键开启脚本
游侠的伤害一定要做到不让Boss碰到你一下，否则会出现被boss打位移或者点不开箱子的问题
需要两个鼠标宏，bilie和gunlun
bilie鼠标宏就是常规的输出宏，游侠的话2放隐身4放索命陷阱，其他职业2放不可阻挡技能
gunlun就是鼠标滚轮往下滚几下的鼠标宏
--]]

function MoveAndPress(x, y)
	Sleep(100)
	MoveMouseTo(x, y)
	Sleep(100)
	PressAndReleaseMouseButton(1)
	Sleep(100)
end


function MouseContrl()
    PressAndReleaseKey("escape")
	Sleep(100)
	MoveAndPress(10792, 36017)
	MoveAndPress(35926, 1944)
	MoveAndPress(37634, 27210)
	MoveAndPress(27594, 63531)
	Sleep(100)
	PressAndReleaseKey("escape")
	Sleep(100)
	PressAndReleaseKey("escape")
end


function OnEvent(event, arg)
	if (event ==   "MOUSE_BUTTON_RELEASED" and arg == 5) then
		-- Mouse Button 5 has been pressed
		k = 0  --开第几个boss箱子从瓦尔申0开始到格里格里5结束
		i = 1.5 --这里是1就是挂10分钟
		second = 600*1000
		--关闭物品标签显示
		Sleep(100)
		PressAndReleaseKey("0")
		Sleep(100)
		MouseContrl()
		Sleep(100)
              
		repeat
			-- Move mouse to 点箱子
			Sleep(4000)
			MoveAndPress(38590, 30247)
			--Sleep(1000)

			
			
			-- --[[当你不需要选箱子开安姐就行的时候，把这下面这选择boss箱子的代码注释掉就行，注释方法是前面--去掉
			-- Move mouse to
			MoveAndPress(11748, 50047)
			Sleep(1000)
			-- 选择boss箱子
			PlayMacro("gunlun")--运行gunlun宏
			Sleep(1000)
			AbortMacro()
			MoveAndPress(12000, 52000-k*5500)
			-- --]]
			
			
			-- Move mouse to 开箱子
			MoveAndPress(11850, 58247)
			Sleep(1000)
			-- Move mouse to 开篝火
			MoveAndPress(25681, 29761)
			Sleep(3500)
			--用霸体技能防止位移
			PressAndReleaseKey("2")
			Sleep(30)
			Sleep(3000)
			-- 输出boss
			MoveMouseTo(33707, 33041)
			Sleep(30)
			PlayMacro("bilie")--运行bilie宏
			Sleep(8000)
			PressAndReleaseKey("4")--放一次索命陷阱保证一定可以开出隐身霸体
			Sleep(100)
			AbortMacro()
			--防止莫名其妙位移，可以实用鼠标右键中止循环（在输出BOSS到开篝火之间按住鼠标右键能停止循环）  
		until IsMouseButtonPressed(3) or GetRunningTime()>= i *second
		--打开物品标签显示
		Sleep(100)
		PressAndReleaseKey("0")
		Sleep(100)
		MouseContrl()
		Sleep(100)
	end
end