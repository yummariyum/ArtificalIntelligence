class node:
    def getCost():
        hCost = 0
        for i in zip(initial, goal):
            if i[0] != i[1]:
                hCost = hCost + 1
            else:
                continue
        return hCost

    def __init__(obj, key, initial, parntNode, gN, moveSelection):
        obj.key = key
        obj.initial = initial
        obj.parntNode = parntNode
        obj.gN = gN
        obj.goal = goal
        obj.moveSelection = moveSelection
        obj.getMoves()

    def getMoves(obj):
        obj.moveSelections = []
        if obj.initial.index(0) == 0:
            obj.moveSelections.extend(('left', 'up'))
        elif obj.initial.index(0) == 1:
            obj.moveSelections.extend(('left', 'right', 'up'))
        elif obj.initial.index(0) == 2:
            obj.moveSelections.extend(('right', 'up'))
        elif obj.initial.index(0) == 3:
            obj.moveSelections.extend(('up', 'down', 'left'))
        elif obj.initial.index(0) == 4:
            obj.moveSelections.extend((
                'up',
                'down',
                'left',
                'right',
            ))
        elif obj.initial.index(0) == 5:
            obj.moveSelections.extend(('right', 'up', 'down'))
        elif obj.initial.index(0) == 6:
            obj.moveSelections.extend(('down', 'left'))
        elif obj.initial.index(0) == 7:
            obj.moveSelections.extend(('left', 'right', 'down'))
        else:
            obj.moveSelections.extend(('right', 'down'))

    def movePiece(obj, moveSelection):
        tempNode = obj.initial[:]
        index0 = tempNode.index(0)
        if moveSelection == 'left':
            repeat = index0 + 1
        elif moveSelection == 'right':
            repeat = index0 - 1
        elif moveSelection == 'up':
            repeat = index0 + 3
        else:
            repeat = index0 - 3
        repeatedVal = initial[repeat]
        tempNode[index0] = repeatedVal
        tempNode[repeat] = 0
        return tempNode, repeatedVal


class queue:
    def __init__(obj, goalState):
        obj.queue = []

    def getNode(obj):
        return obj.queue[0]


class Tree:
    def __init__(obj, newNode, goalState, iterateDeep):
        obj.goalState = newNode.goal
        obj.currNode = newNode
        obj.root = newNode
        obj.iterateDeep = iterateDeep
        obj.key = 0
        obj.moveCounter = 0
        obj.tree = {}
        obj.queue = queue(obj.goalState)
        obj.queue.queue.append(obj.root)
        obj.visited = []
        obj.depthCount = 0
        obj.limit = 0
        obj.tree[0] = obj.root
        obj.BFS()

    def BFS(obj):
        obj.currNode = obj.queue.getNode()
        while obj.queue:
            QueueEle = []
            QueueEle.append(len(obj.queue.queue))
            if obj.currNode.initial != obj.goalState:
                if obj.iterateDeep:
                    if obj.depthCount > obj.limit:
                        obj.limit = obj.limit + 1
                        obj.key = 0
                        obj.moveCounter = 0
                        obj.tree = {}
                        obj.queue = queue(obj.goalState)
                        obj.queue.queue.append(obj.root)
                        obj.visited = []
                        obj.depthCount = 0
                        obj.currNode = obj.root
                    else:
                        pass
                else:
                    pass
                if obj.currNode.initial not in obj.visited:
                    obj.visited.append(obj.currNode.initial[:])
                    obj.moveCounter = obj.moveCounter + 1
                    for moveSelection in obj.currNode.moveSelections:
                        obj.key = obj.key + 1
                        newinitial, gN = obj.currNode.movePiece(moveSelection)
                        gN = gN + obj.currNode.gN
                        key = obj.key
                        initial = newinitial
                        parntNode = obj.currNode.key
                        tempNode = node(key, initial, parntNode, gN,
                                        moveSelection)
                        obj.tree[obj.key] = tempNode
                        sca = 0
                        sort = 'gN'
                        for i in obj.queue.queue:
                            if i.initial == tempNode.initial:
                                if getattr(i, sort) > getattr(tempNode, sort):
                                    del obj.queue.queue[sca]
                                else:
                                    sca = sca + 1
                            else:
                                sca = sca + 1
                        obj.queue.queue.append(tempNode)
                    obj.depthCount = obj.depthCount + 1
                    obj.currNode = obj.queue.getNode()
                else:
                    idx = 0
                    del obj.queue.queue[idx]
                    obj.currNode = obj.queue.getNode()
            else:
                break
        for k, v in obj.tree.items():
            if v.initial == obj.goalState:
                kth = k
                break
            else:
                continue
        pathIdent = [kth]
        while kth != 0:
            pathIdent.insert(0, obj.tree[kth].parntNode)
            kth = pathIdent[0]
        for i in pathIdent:
            print(' Move:', obj.tree[i].moveSelection, '\n', 'Total Cost:',
                  obj.tree[i].gN, '\n', '---------\n',
                  obj.tree[i].initial[0:3], '\n', obj.tree[i].initial[3:6],
                  '\n', obj.tree[i].initial[6:], '\n', '---------\n')
        print('Total Moves Made: ', len(pathIdent) - 1)


goal = [1, 2, 3, 4, 5, 6, 0, 7, 8]
initial = [2, 3, 6, 1, 5, 0, 4, 7, 8]
flag = 0
key = 0
parntNode = 0
gN = 0
depth = 0
moveSelection = 'Initial State'
objNode = node(key, initial, parntNode, gN, moveSelection)
test = Tree(objNode, goal, flag)
