local blocks = 1
local total = 0

function report ()
    --print(os.getComputerLabel() .. " has measured " .. blocks .. " blocks.")
    total = blocks
    blocks = 1
    return total
end
function forward ()
    while turtle.forward() do
      blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.back()  
    end
    return report()
end
function right()
    turtle.turnRight()
    forward()
    return report()
end
function left()
    turtle.turnLeft()
    forward()
    return report()
end
function up()
     while turtle.up() do
        blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.down()  
    end
    return report()
end
function down()
    while turtle.down() do
        blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.up()  
    end
    return report()
end
function back()
    while turtle.back() do
        blocks = blocks + 1
    end
    for i = 1, blocks - 1, 1 do
        turtle.forward()  
    end
    return report()
end
