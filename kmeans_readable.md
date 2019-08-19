

```python
ip = [1,3,5,49,50,200,250]
k = 3
# taking random vals
centroids = [ip[i] for i in range(k)]
centroids
```




    [1, 3, 5]




```python
def diff(x,y):
    return abs(x-y)

def meancalc(clusterlist):
    total = 0
    for num in clusterlist:
        total = total + num
    mean = total/len(clusterlist)
    return mean

def clustering(cluster_lol, ip):
    mean_list = [[] for i in range(len(cluster_lol))]
    for i in range(len(ip)):
        # initialization
        low_ind = 0
        low_val = cluster_lol[0][i]
        for j in range(1,len(cluster_lol)):
            if cluster_lol[j][i] < low_val:
                low_val = cluster_lol[j][i]
                low_ind = j
        mean_list[low_ind].append(ip[i])
    return mean_list

# sam_clol = [[0,2,3,48,49,199,249],[2,0,2,46,47,197,247],[4,2,0,44,45,195,245]]
# clustering(sam_clol, ip)
def is_c_changed(new_centroids, old_centroids):
    for i in range(len(old_centroids)):
        if old_centroids[i] != new_centroids[i]:
            return True
    return False
```


```python
while True:
    interim_mat = []
    for c in centroids:
        tmp_list = []
        for num in ip:
            diff_val = diff(c,num)
            tmp_list.append(diff_val)
        interim_mat.append(tmp_list)
    cluster_mat = clustering(interim_mat, ip)
    new_centroids = []
    for i_list in cluster_mat:
        cal_mean = meancalc(i_list)
        new_centroids.append(cal_mean)
    #check if centroids changed or not
    if is_c_changed(new_centroids, centroids):
        centroids = new_centroids
    else:
        break

# print the cluster_mat
c_ind = 0
for i_list in cluster_mat:
    print(centroids[c_ind], " : ", i_list)
    c_ind = c_ind + 1
```

    3.0  :  [1, 3, 5]
    49.5  :  [49, 50]
    225.0  :  [200, 250]

