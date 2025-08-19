## Select

- **`d3.select()`** → used to **select a single HTML element or tag** from the document.
- **`d3.select('#main')`** → selects the **element with `id="main"`**.
    - Returns the **HTML node wrapped in a D3 selection**, which you can then manipulate.
- **D3.js** → a **JavaScript library** for creating dynamic and interactive **data visualizations** in the browser.
- **Example of usage:**

```jsx
d3.select('#main')
  .text("Hello D3!")      // changes text
  .style("color", "blue") // changes text color
  .style("font-size", "24px"); // changes font size
 
 once the d3 is used all the previous elements are updated,
 Think of it like a wrapper around the element — any method you call affects the wrapped  element(s) directly.
```

---

## Append

- **`d3.append()`** → used to **create a new element inside the selected (wrapped) element**.
- **`d3.append('h2')`** → adds a new `<h2>` element **inside the selected element**.
- **Example:**

```jsx
// Select the <body> and add a new <h2> element inside it
d3.select('body')
  .append('h2')
  .text("Hello D3!");  // sets the text inside the new <h2>
```

- **What happens:**
    - A new `<h2>` element is created **inside the `<body>`**.
    - You can then chain methods like `.text()`, `.style()`, or `.attr()` to modify it.

💡 **Tip:** `append()` **does not replace existing elements** — it **adds a new child element** to the wrapped selection.

---

## SelectAll

- `d3.selectAll()` → is used for selecting all the elements within the specified tag and do the same thing as select element.

---

## Data and enter

- `data()` → bind your dataset to elements.
- `enter()` → represents missing elements for data.
    - It **represents the data items that don’t yet have corresponding elements in the DOM(data object model)**
- Eg following syntax:
    
    ```jsx
    const dataset = [10, 20, 30];
    // Suppose there are 0 <p> tags in the HTML
    d3.select('body')
    .selectAll('p')   // selects 0 existing <p> elements
    .data(dataset)    // binds 3 data items
    .enter()          // enter selection = all 3 data items
    .append('p')      // create 3 new <p> tags
    .text('USD');    // set their text to 10, 20, 30
    think of it as loop that keeps running till dataset.
    ```
    
- Lets suppose you want to access the element within the dataset how should we do it:
    
    ```jsx
    const dataset = [10, 20, 30];
    // Suppose there are 0 <p> tags in the HTML
    d3.select('body')
    .selectAll('p')   // selects 0 existing <p> elements
    .data(dataset)    // binds 3 data items
    .enter()          // enter selection = all 3 data items
    .append('p')      // create 3 new <p> tags
    .text( d=>d + 'USD');    // set their text to 10, 20, 30
    
    d=>d this is used for accessing the data set elements its not necessary that it has
    to be d it can be any value.
    ```
    

---

## Style

- You can also perform styling in your elements
- Syntax:
    
    ```jsx
    .style('font-family', 'time new roman')
    the comma seperator acts as an argument.
    ```
    

---

## Styling based on condition

- Syntax:

```jsx
.style('color', d=>d <= 20 ? 'red' : 'green')
```

---

## Attr

- When we need to use multiple inline styling effects we need to use `attr()`
- `attr()` is used for attribute function.
- For eg:
    
    ```jsx
    .attr('class', 'container')
    the class(label) is same every time, only the container changes.
    ```
    

---

## Making a bar chart using the dataset

```jsx
.style('height', d => d + 'px');
means:
For each data point d in your dataset,
Set the height CSS property of the corresponding <div> to d pixels.
So if your dataset is:
[12, 31, 22]
the generated <div> heights will be:
12px
31px
22px
```

---

## Changing the bar chart

- `margin` → used to add space
    
    ```jsx
    .style('height', d => d * 5 + 'px');
    means:
    For each data point d in your dataset,
    Set the height CSS property of the corresponding <div> to d pixels.
    So if your dataset is:
    [12, 31, 22]
    the generated <div> heights will be:
    12px
    31px
    22px
    ```
    
- Multiplying the data set with 5 allows them to zoom in it doesn’t changes the data rather it scales it up.

---

## Displaying shapes using SVG

- SVG stands for scalable vector graphics.
- Like rectangle <rect>
- There are four attributes with rectangle, it has 4 corners:
    - X
    - Y
    - Height
    - Width

---

## **Dynamically Set the Coordinates for Each Bar**

- Syntax:
    
    ```jsx
    .attr('x', (d, i) => i * 30)
    over here d is the total datset and i is the index, as a loop the i goes from 0 to 12.
    ```
    
- If we are changing the data we use `d`

---

## Invert SVG elements

- To invert the bar chart we use the y coordinate. If the y is 1 then the SVG is 100
- Formula:
    - y = h - d * m
    - where h is the height of SVG
    - d is the dataset
    - m is the main constant scale.

---

## Changing the color

- To change the color we use `fill()` method
- Syntax:
    
    ```jsx
    .attr('fill', 'red')
    ```
    
---

## Hover effect

- For some effects we need to use the style sheet.

---

## Tool tip

- Tooltip is used for showing more  information about the page once the mouse is hovered.
- It uses `title` method for pairing.
- Syntax:
    
    ```
     .append('title')
          .text((item) =>
          {
            return item
          })
    ```
    

---

## Creating a linear scale

- `scales` are functions that helps us to plot raw data on the pixel scree using SVG.
- The method used for it is `scaleLinear()`

---

## Domain and Range

- Data values from 10 to 500, if this is the input information then its known as `domain`
- Data values from 10 unit to 500 units, if this is the output information then its known as `range` and they are mostly around `x` plot.
    
    ```jsx
    const scale = d3.scaleLinear();
    scale.domain([250, 500]);   // input values go from 250 → 500
    scale.range([10, 150]);     // output values go from 10 → 150
    const output = scale(50);   // 50 is **below the domain**
    D3 linearly interpolates based on the domain.
    ```
    

Formula for linear scaling:
![image.png](attachment:8fdad644-1c64-46f9-974a-4ca2dac0dae3:image.png)


---

## Max and Min

- Syntax
    
    ```jsx
    const positionData = [
    [1, 7, -4],
    [6, 3, 8],
    [2, 9, 3]
    ];
    positionData is a 2D array → an array of arrays.
    ```
    
- Each element d in d3.max(positionData, d => d[2]) represents one row (an inner array).
    - d3.max(array, accessor)
- Loops through every element in array.
- For positionData, it loops through each row:
    - d = [1, 7, -4] → first row
    - d = [6, 3, 8] → second row
    - d = [2, 9, 3] → third row
    - d => d[2]
    - For each row, it accesses the third element (index 2) of that row.
    - So it evaluates: -4, 8, 3
- `d3.max()`
- Returns the largest value among -4, 8, 3 → which is 8.

---
