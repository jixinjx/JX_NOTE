# 方法一

```
parentDiv {
  display:flex;
  flex-direction:row;
} 
.childDiv {
flex:1;
}
```

# 方法二

```
.test { 
    display: flex; 
    flex-flow: row wrap; 
    justify-content: space-around; 
} 
.test > div { 
    margin-top: 10px; 
    padding: 20px; 
    background-color: #FF0000; 
} 
```