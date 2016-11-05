--[[
    As seen in The ComputerCraft Challenge [youtube.com/bwochinski]
	This program will mine in vertical shafts down to bedrock, checking the walls of the shaft.
	Shafts are staggered so the turtle will view every block if the pattern is continued.
	Set "consoleID" to the id of a computer listening on rednet to get remote status messages.
	** Prep the Turtle before running! **
	Slots 1,2,3 are for blocks not to mine (smooth stone, gravel, dirt)
	Slot 15 is the block to backfill holes (recommend cobble)
	Slot 16 is for fuel
]]--
isWireless = false
consoleID = 1
depth = 0

function fuel()
	if turtle.getFuelLevel() <= depth + 10 then
		turtle.select(16)
		turtle.refuel(1)
		if isWireless then rednet.send(consoleID,"Refueled. Fuel level: "..turtle.getFuelLevel()) end
	end
end

function isValuable() 
	if turtle.detect() == false then 
		return false 
	end 
	for i=1,3 do 
		turtle.select(i) 
		if turtle.compare() then 
			return false 
		end 
	end 
	return true 
end

function checkWalls(dp)
	for j=1,4 do
		if isValuable() then
			if isWireless then rednet.send(consoleID,"Found ore at depth "..dp) end
			turtle.dig()
		end
		turtle.turnRight()
	end
end

------ ( Program Start ) ------

if isWireless == true then
   rednet.open("right")
end

term.clear()
term.setCursorPos(1,1)
print("Ben's Simple Turtle Miner")
print("-------------------------")

term.write("Go on mining run? (y/n): ")

while read() == "y" do
	
	depth = 0
	print("Commencing mining.")
	if isWireless then rednet.send(consoleID,"Commencing mining.") end
	
	fuel()
	turtle.digDown()
	for st=1,2 do
		turtle.down()
		depth = depth + 1
		turtle.digDown()
	end
	
	-- plug entrance hole
	turtle.select(15)
	turtle.placeUp()
	
	while not turtle.detectDown() do
		fuel()
		turtle.down()
		depth = depth + 1
		if isWireless and depth%10==0 then
			rednet.send(consoleID,"At depth "..depth)
		end
		checkWalls(depth)
		turtle.digDown()
	end
	
	if isWireless then rednet.send(consoleID,"Moving to next shaft location...") end
	
	for mv=1,6 do
		fuel()
		turtle.up()
		depth = depth - 1
	end
	
	-- move forward 2 blocks
	for z=1,2 do
		fuel()
		while not turtle.forward() do
			turtle.dig()
			sleep(.8)
		end
	end
	
	-- turn right and move one block
	turtle.turnRight()
	fuel()
	while not turtle.forward() do
		turtle.dig()
		sleep(.8)
	end
	turtle.turnLeft()
	
	-- go down to bedrock
	turtle.digDown()
	while not turtle.detectDown() do
		fuel()
		turtle.down()
		depth = depth + 1
		turtle.digDown()
	end
	
	if isWireless then rednet.send(consoleID,"Returning to surface!") end
	
	for k=depth,3,-1 do
		checkWalls(k)
		turtle.digUp()
		fuel()
		while not turtle.up() do
			turtle.digUp()
			sleep(.5)
		end
		if isWireless and k%10 == 0 then
			rednet.send(consoleID,"At depth "..k)
		end
	end
	
	fuel()
	turtle.digUp()
	turtle.up()
	turtle.digUp()
	turtle.up()
	
	-- fill exit hole
	turtle.select(15)
	turtle.placeDown()
	
	turtle.forward()
	turtle.forward()
	turtle.turnRight()
	turtle.forward()
	turtle.turnLeft()
	
	term.write("Go on mining run? (y/n): ")
end

print("Cancelled mining.")

if isWireless then rednet.close("right") end
