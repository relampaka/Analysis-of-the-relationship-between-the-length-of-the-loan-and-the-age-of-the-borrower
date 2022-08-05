# German loans
import numpy as np
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score
from matplotlib import pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
trans_set=pd.read_csv('german_credit.csv', sep=',',header=0)
Data=trans_set.values
x = Data[:,2]
y = Data[:,13]
z = Data[:,20]
def scatter3d(x,y,z,c):
    fig = plt.figure(figsize=(8, 8))
    ax = fig.add_subplot(111, projection='3d')
    ax.scatter(x, y,z,c=c)
    ax.set_title('Loans in Germany')
    ax.set_xlabel('Length of credit (months)')
    ax.set_ylabel('Age (years)')
    ax.set_zlabel('Foreigner (no/yes)')
    plt.show()
    print(type(x))
    scatter3d(x,y,z,'blue')
    Clients = Data
Clients = np.delete(Clients, np.s_[0:2], axis=1)
Clients = np.delete(Clients, np.s_[1:11], axis=1)
Clients = np.delete(Clients, np.s_[2:8], axis=1)
kmeans = KMeans(n_clusters=5, random_state=0).fit(Clients)
portraits = kmeans.cluster_centers_
for x in range (5):
    if(round(portraits[x][2])==1):
        resident = 'Citizen '
    else:
        resident ='Visitor '
    months = int(round(portraits[x][0]))
    years = round((months/12),1)
    print(resident+'at the age of '+ str(int(round(portraits[x][1])))+' years and a term loan '+str(months)+'months ('+str(years)+' years).')
    labels = kmeans.labels_
    color = list(range(len(Data)))

for x in range(len(Data)):
    if labels[x] == 0:
        color[x]= 'red'
    elif labels[x]== 1:
        color[x] ='yellow'
    elif labels[x] == 2:
        color[x] ='green'
    elif labels[x] == 3:
        color[x] ='blue'
    else:
        color[x]='black'
        x = Clients[:,0]
y = Clients[:,1]
z = Clients[:,2]
scatter3d(x,y,z,c=labels)
