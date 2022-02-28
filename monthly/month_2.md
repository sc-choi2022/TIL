**CSS 우선순위**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
  <link rel="stylesheet" href="style.css">
  <title>Document</title>
  <style>
    #first-box.red{
      color:red;
    }
    #second-box{
      color:violet;
    }
    .black{
      color:black
    }
    .blue{
      color:blue;
    }
  </style>
</head>
<body>
  <div id="first-box">
    <h1 class="blue red black">HELLO</h1>
  </div>
  <div id="second-box">
    <h1 class="blue black">WORLD</h1>
  </div>
</body>
```

HELLO

WORLD

모두 blue가 된다.



```python
def find(arr):
    for a in range(N):
        for b in range(N):
            if arr[a][b] == 2:
                i = a
                j = b
    return [i, j]

T = int(input())

for case in range(1, T+1):
    # NxN 행렬의 N
    N = int(input())
    # NxN 행렬의 값을 받는 리스트 arr
    arr = [list(map(int, input().split())) for _ in range(N)]
    cnt = 0

    di = [0, 1, 0, -1]
    dj = [1, 0, -1, 0]

    for d in range(4):
        temp = find(arr)
        i = temp[0]
        j = temp[1]

        while True:
            ni = i + di[d]
            nj = j + dj[d]
            if 0<= ni < N and 0<= nj <N and arr[ni][nj] == 0:
                i = ni
                j = nj
                arr[i][j] = 1
            elif 0<= ni < N or 0<= nj <N or arr[ni][nj] == 1:
                break

    for ii in range(N):
        for jj in range(N):
            if arr[ii][jj] == 0:
                cnt +=1
    print(f'#{case} {cnt}')
```

