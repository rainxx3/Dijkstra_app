# Dijkstra_app
~~~
import tkinter as tk
root = tk.Tk()

startnode = tk.StringVar(root)
endnode = tk.StringVar(root)

listStations = [
    'Bank',
    'Blackfriars',
    'Cannon Street',
    'Chancery Lane',
    'Charing Cross',
    'Covent Garden',
    'Embankment',
    'Goodge Street',
    'Holborn',
    'Leicester Square',
    'London Bridge',
    'Mansion House',
    "St Paul's",
    'Temple',
    'Tottenham Court Road',
]


start = startnode
end = endnode


graph = {'a':{'b':10,'c':3},'b':{'c':1,'d':2},'c':{'b':4,'d':8,'e':2},'d':{'e':7},'e':{'d':9}}




def run_algorithm():
    def algorithm(graph,start,end):
        shortest_distance = {}
        parents = {}
        unseenNodes = graph
        infinity = 9999
        path = []
        for node in unseenNodes:
            shortest_distance[node] = infinity
        shortest_distance[start.get()] = 0

        while unseenNodes:
            minNode = None
            for node in unseenNodes:
                if minNode is None:
                    minNode = node
                elif shortest_distance[node] < shortest_distance[minNode]:
                    minNode = node

            for childNode, weight in graph[minNode].items():
                if weight + shortest_distance[minNode] < shortest_distance[childNode]:
                    shortest_distance[childNode] = weight + shortest_distance[minNode]
                    parents[childNode] = minNode
            unseenNodes.pop(minNode)
################################### im geting an error here. 
###goes straight to path not founf.
###sometimes its an attribute error
        currentNode = endnode
        while currentNode != start:
            try:
                path.insert(0,currentNode)
                currentNode = parents[currentNode.get()] ###mainly this line
            except KeyError:
                print('path not found')
                break

        path.insert(0,start)
        if shortest_distance[end.get()] != infinity:
            print('Shortest dist ' + str(shortest_distance[end]))
            print('and path is ' + str(path))
#################################################

    algorithm(graph, startnode, endnode)
  
#interface
canvas = tk.Canvas(root, height=500, width=600)
canvas.pack()

frame = tk.Frame(root, bg='#FFEFD5')
frame.place(relwidth=0.8, relheight=0.8, relx=0.1, rely=0.1)

frame1 = tk.Frame(frame, bg='#00CED1', bd=10)
frame1.place(relwidth=0.9, relheight=0.15, relx=0.05, rely=0.3)

frame2 = tk.Frame(frame, bg='#00CED1', bd=10)
frame2.place(relwidth=0.9, relheight=0.15, relx=0.05, rely=0.5)

label = tk.Label(frame1, text='Select Starting Point', font=40)
label.place(relx=0, rely=0, relheight=1, relwidth=0.4)

label2 = tk.Label(frame2, text='Select Finishing Point', font=40)
label2.place(relx=0, rely=0, relheight=1, relwidth=0.4)

label3 = tk.Label(frame, text='Plan a Zone 1 Journey', font=40)
label3.place(relx=0.2, rely=0.1, relheight=0.1, relwidth=0.6)

menu1 = ttk.OptionMenu(root, *listStations)
menu1.place(relx=0.55, rely=0.35, relheight=0.07, relwidth=0.3)

menu2 = ttk.OptionMenu(root, *listStaions)
menu2.place(relx=0.55, rely=0.55, relheight=0.07, relwidth=0.3)

button = tk.Button(frame, text='Go!', bg='#00CED1', command=run_algorithm)
button.place(relx=0.35, rely=0.8, relheight=0.07, relwidth=0.3)

root.mainloop()
~~~
