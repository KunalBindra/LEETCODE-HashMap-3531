# LEETCODE-HashMap-3531
```
n = 3
buildings = [[1,1], [1,2], [2,1], [2,2]]
```

---

# 🧠 Phase 1: Build the maps (YMMX and XMMY)

### **YMMX → for each y: min/max x**

### **XMMY → for each x: min/max y**

We iterate over each building:

---

## **1) building = [1,1] → x=1, y=1**

### YMMX:

* y=1 not present → add (minX=∞, maxX=-∞)
* update with x=1 → minX=1, maxX=1
  ⇒ **YMMX = {1: [1,1]}**

### XMMY:

* x=1 not present → add (minY=∞, maxY=-∞)
* update with y=1 → minY=1, maxY=1
  ⇒ **XMMY = {1: [1,1]}**

---

## **2) building = [1,2] → x=1, y=2**

### YMMX:

* y=2 not present → add (∞, -∞)
* update with x=1 → [1,1]
  ⇒ **YMMX = {1:[1,1], 2:[1,1]}**

### XMMY:

* x=1 already exists ([1,1])
* update with y=2 → minY=1, maxY=2
  ⇒ **XMMY = {1:[1,2]}**

---

## **3) building = [2,1] → x=2, y=1**

### YMMX:

* y=1 exists ([1,1])
* update with x=2 → now [1,2]

### XMMY:

* x=2 not present → add (∞, -∞)
* update with y=1 → [1,1]

⇒ **YMMX = {1:[1,2], 2:[1,1]}**
⇒ **XMMY = {1:[1,2], 2:[1,1]}**

---

## **4) building = [2,2] → x=2, y=2**

### YMMX:

* y=2 has [1,1]
* update with x=2 → becomes [1,2]

### XMMY:

* x=2 has [1,1]
* update with y=2 → becomes [1,2]

⇒ **Final maps:**

### **YMMX**

| y | minX | maxX |
| - | ---- | ---- |
| 1 | 1    | 2    |
| 2 | 1    | 2    |

### **XMMY**

| x | minY | maxY |
| - | ---- | ---- |
| 1 | 1    | 2    |
| 2 | 1    | 2    |

---

# 🧠 Phase 2: Count covered buildings

A building at (x, y) is "covered" if:

```
minX(y) < x < maxX(y)
AND
minY(x) < y < maxY(x)
```

For this grid, that means:

* For y=1 → x must be strictly between 1 and 2 → impossible
* For y=2 → same
* For x=1 → y must be strictly between 1 and 2
* For x=2 → same

Strict inequality kills everything.

Let’s check each:

---

## Check (1,1)

* xr = YMMX.get(1) = [1,2]
* yr = XMMY.get(1) = [1,2]
* Need: 1 < 1 < 2 ❌

**Not covered**

---

## Check (1,2)

* Need: 1 < 1 < 2 ❌

**Not covered**

---

## Check (2,1)

* Need: 1 < 2 < 2 ❌

**Not covered**

---

## Check (2,2)

* Need: 1 < 2 < 2 ❌

**Not covered**

---

# ✅ **Final Result = 0**

No building is strictly inside a rectangle formed by others because all buildings lie on the boundary of the 2×2 square.

---

# 🎉 Final Answer: **0**
