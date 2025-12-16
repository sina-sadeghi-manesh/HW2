class problem():
    def __init__(self, initial_state, goal_state):
        self.initial_state = initial_state
        self.goal_state = goal_state
        
    
    def result(self, state, action):
        new_state = None
        return new_state
    
    def goal_test(self, state):
        if isinstance(self.goal_state, list):
            return (state in self.goal_state)
        else:
            return state == self.goal_state
        
    def successor(self, state):
        raise NotImplementedError(" Successor not implemented")
        
    def path_cost(self, c, state_1, state_2, action):
        return (c + 1)


class state():
    def __init__(self, colums):
        self.state = [[] for i in range((colums))]


    
    
class hanoi_tower(problem):
    def __init__(self, initial_state, goal_state):
        self.initial_state = initial_state
        self.goal_state = goal_state
        super().__init__(initial_state, goal_state)
    
    def successor(self, state):
        moves = []
        for i in range(len(state)):
            if len(state[i]) == 0:
                continue
            for j in range(3):
                if i == j:
                    continue
                if len(state[j]) == 0 or state[i][-1] < state[j][-1]:
                    moves.append((i,j))
        return moves
    
    def result(self, state, action):
        i , j = action
        disk = state[i].pop()
        state[j].append(disk)
        return state
    
    def goal_test(self, state):
        return state == self.goal_state
        
    
'''
my = hanoi_tower([[3,2,1],[],[]], [[],[],[3,2,1]])
list_of_actions = my.successor(my.initial_state)
print(list_of_actions)  
'''
