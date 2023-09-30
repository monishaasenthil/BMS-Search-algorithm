# BMS-Search-algorithm
//British museum search this algorithm writes each nodes immediate neighbours, lexicographical sorting-comparing each characters from left to right, doesn't expand at the //tail, stops at the goal, this algorithm finds all possible paths from source to destination.
def find_paths_between(graph, start, end, path=[]):
    path = path + [start]
    if start == end:
        return [path]
    if start not in graph:
        return []
    paths = []
    for node in graph[start]:
        if node not in path:
            new_paths = find_paths_between(graph, node, end, path)
            for new_path in new_paths:
                paths.append(new_path)
    return paths

def all_paths(graph, start, end):
    paths = find_paths_between(graph, start, end)
    sorted_paths = sorted(paths, key=lambda x: (len(x), x))
    return sorted_paths

# Define your graph as a dictionary of adjacency lists
graph = {
    's': ['a', 'b'],
    'a': ['d'],
    'b': ['a'],
    'c': ['e'],
    'd': ['g'],
    'g': []
}

source = 's'
destination = 'g'

paths = all_paths(graph, source, destination)

if paths:
    print("Paths from", source, "to", destination, "in lexicographical order:")
    for path in paths:
        print("->".join(path))
else:
    print("No path found from", source, "to", destination)
