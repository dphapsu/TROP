tArgs = {...}
local dir = tArgs[1]
local blocks = 1

function forward ()
    while turtle.forward() do
      blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.back()  
    end
end

if dir == "right" then
    turtle.turnRight()
    forward()
elseif dir == "left" then
    turtle.turnLeft()
    forward()
elseif dir == "up" then
    while turtle.up() do
        blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.down()  
    end
elseif dir == "down" then
    while turtle.down() do
        blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.up()  
    end
else
    forward()
end

print(os.getComputerLabel() .. " has measured " .. blocks .. " blocks.")