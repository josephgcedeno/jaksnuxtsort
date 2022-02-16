<template>
  <div class="container">
    <div class="dataset">
      <input type="text" ref="inputval" value="" name="datasetval" placeholder="Input Dataset">
      <button @click="btnClicked" class="btn btn-outline">Sort</button>
    </div>
    <div class="card-grid">
        <div class="card card-shadow" v-for="sort in sorts" :key="sort">
          <div class="card-header">{{sort}}</div>
          <div class="card-body">
            <section class="data-container" ref="containerdiv">
              <div 
                :style="[
                    {'height': ` ${value * 3}px`},
                    {'transform': 'translateX('+(index * 35)+'px) '},
                ]"
                class="bar" 
                 v-for="(value, index) in datasetval"  
                :key="index"
                >
                <label class="bar_id">{{value}}</label>
               
              </div>
            </section>
          </div>
        </div>
      </div>
  </div>

</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'

@Component({
  head() {
    return {
      title: 'Jaks template',
    }
  }
})

export default class Index extends Vue {

  //data
  sorts:string[] =[
    "SelectionSort",
      "BubbleSort",
      "InsertionSort",
      "MergeSort",
      "QuickSort",
    "Heap Sort"
  ];
  container:any;
  bubblesortcontainer:any;
  insertionsortcontainer:any;
  mergesortcontainer:any;
  quicksort:any;
  heapsort:any;


  //datasetval:string ='846335478';
  datasetval:number[] =[9,8,1,5,6];

  // * * Methods
  btnClicked(){
      this.datasetval = []
      setTimeout(()=>{
        let inputval:any = this.$refs.inputval;
        this.datasetval = inputval.value.split(",");
      
         setTimeout(this.callSortingFunc,2000);
      },1000);

  }
  callSortingFunc(){
   // alert("Start Sorting")
    this.SelectionSort();
    this.BubbleSort();
    this.InsertionSort();
    this.HeapSort(20);
  }
  
  mounted():void{
     this.container = this.$refs.containerdiv;
     this.bubblesortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(2) > div.card-body > section");
     this.insertionsortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(3) > div.card-body > section");
     this.mergesortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(4) > div.card-body > section");
     this.quicksort = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(5) > div.card-body > section");
     this.heapsort = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(6) > div.card-body > section");
     setTimeout(this.callSortingFunc,2000);
  }
  // selection sort
  async SelectionSort(delay = 300) {

    let bars:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(1) > div.card-body > section > div");
    // Assign 0 to min_idx
    var min_idx = 0;
    for (var i = 0; i < bars.length; i += 1) {

      // Assign i to min_idx
      min_idx = i;

      // Provide darkblue color to the ith bar
      bars[i].style.backgroundColor = "darkblue";
      for (var j = i + 1; j < bars.length; j += 1) {

      // Provide red color to the jth bar
      bars[j].style.backgroundColor = "red";
        
      // To pause the execution of code for 300 milliseconds
      await new Promise((resolve:any) =>
        setTimeout(() => {
        resolve();
        }, 300)
      );

      // To store the integer value of jth bar to var1
      var val1 = parseInt(bars[j].childNodes[0].innerHTML);

      // To store the integer value of (min_idx)th bar to var2
      var val2 = parseInt(bars[min_idx].childNodes[0].innerHTML);
        
      // Compare val1 & val2
      if (val1 < val2) {
        if (min_idx !== i) {

        // Provide skyblue color to the (min-idx)th bar
        bars[min_idx].style.backgroundColor = " rgb(24, 190, 255)";
        }
        min_idx = j;
      } else {

        // Provide skyblue color to the jth bar
        bars[j].style.backgroundColor = " rgb(24, 190, 255)";
      }
      }

      // To swap ith and (min_idx)th bar
      var temp1 = bars[min_idx].style.height;
      var temp2 = bars[min_idx].childNodes[0].innerText;
      bars[min_idx].style.height = bars[i].style.height;
      bars[i].style.height = temp1;
      bars[min_idx].childNodes[0].innerText = bars[i].childNodes[0].innerText;
      bars[i].childNodes[0].innerText = temp2;
      
      // To pause the execution of code for 300 milliseconds
      await new Promise((resolve:any) =>
      setTimeout(() => {
        resolve();
      }, 300)
      );

      // Provide skyblue color to the (min-idx)th bar
      bars[min_idx].style.backgroundColor = " rgb(24, 190, 255)";

      // Provide lightgreen color to the ith bar
      bars[i].style.backgroundColor = " rgb(49, 226, 13)";
  }

  }
  // bubble sort
  // Promise to swap two blocks
  swap(el1:any, el2:any) {
      return new Promise((resolve:any) => {
    
          // For exchanging styles of two blocks
          var temp = el1.style.transform;
          el1.style.transform = el2.style.transform;
          el2.style.transform = temp;
    
          window.requestAnimationFrame(() => {
              // For waiting for .25 sec
              setTimeout(() => {
                  this.bubblesortcontainer.insertBefore(el2, el1);
                  resolve();
              }, 250);
          });
      });
  }
  // Asynchronous BubbleSort function
  async BubbleSort(delay = 100) {
      var blocks:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(2) > div.card-body > section > div");
    
      // BubbleSort Algorithm
      for (var i = 0; i < blocks.length; i += 1) {
          for (var j = 0; j < blocks.length - i - 1; j += 1) {
    
              // To change background-color of the
              // blocks to be compared
              blocks[j].style.backgroundColor = "#FF4949";
              blocks[j + 1].style.backgroundColor = "#FF4949";
    
              // To wait for .1 sec
              await new Promise((resolve:any) =>
                  setTimeout(() => {
                      resolve();
                  }, delay)
              );
    
              var value1 = Number(blocks[j].childNodes[0].innerHTML);
              var value2 = Number(blocks[j + 1]
                          .childNodes[0].innerHTML);
    
              // To compare value of two blocks
              if (value1 > value2) {
                  await this.swap(blocks[j], blocks[j + 1]);
                  blocks = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(2) > div.card-body > section > div");
              }
    
              // Changing the color to the previous one
              blocks[j].style.backgroundColor = "#6b5b95";
              blocks[j + 1].style.backgroundColor = "#6b5b95";
          }
    
          //changing the color of greatest element 
          //found in the above traversal
          blocks[blocks.length - i - 1]
                  .style.backgroundColor = "#13CE66";
      }
  }
  async InsertionSort(delay = 600) {
      let bars:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(3) > div.card-body > section > div");
      
      // Provide lightgreen colour to 0th bar
      bars[0].style.backgroundColor = " rgb(49, 226, 13)";
      for (var i = 1; i < bars.length; i += 1) {
        // Assign i-1 to j
        var j = i - 1;
        // To store the integer value of ith bar to key 
        var key = 
        parseInt(bars[i].childNodes[0].innerHTML);
        // To store the ith bar height to height
        var height = bars[i].style.height;
        // For selecting section having id "ele"

        //gitago nako uwu
        // var barval:any=document.getElementById("ele")
        // // For dynamically Updating the selected element
        //   barval.innerHTML=
        //   `<h3>Element Selected is :${key}</h3>`;
      
        //Provide darkblue color to the ith bar 
        bars[i].style.backgroundColor = "darkblue";
          
        // To pause the execution of code for 600 milliseconds
        await new Promise((resolve:any) =>
        setTimeout(() => {
          resolve();
        }, 600)
      );
      
        // For placing selected element at its correct position 
        while (j >= 0 && parseInt(bars[j].childNodes[0].innerHTML) > key) {
            
          // Provide darkblue color to the jth bar
          bars[j].style.backgroundColor = "darkblue";
            
          // For placing jth element over (j+1)th element
          bars[j + 1].style.height = bars[j].style.height;
          bars[j + 1].childNodes[0].innerText = 
          bars[j].childNodes[0].innerText;
      
          // Assign j-1 to j
          j = j - 1;
      
          // To pause the execution of code for 600 milliseconds
          await new Promise((resolve:any) =>
            setTimeout(() => {
              resolve();
            }, 600)
          );
            
          // Provide lightgreen color to the sorted part
          for(var k=i;k>=0;k--){
            bars[k].style.backgroundColor = " rgb(49, 226, 13)";
          }
        }
      
        // Placing the selected element to its correct position
        bars[j + 1].style.height = height;
        bars[j + 1].childNodes[0].innerHTML = key;
          
        // To pause the execution of code for 600 milliseconds
        await new Promise((resolve:any) =>
          setTimeout(() => {
            resolve();
          }, 600)
        );
          
        // Provide light green color to the ith bar
        bars[i].style.backgroundColor = " rgb(49, 226, 13)";
      }

  }
  async Heapify(n:any, i:any) {
    var blocks:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(6) > div.card-body > section > div");
    var largest = i; // Initialize largest as root
    var l = 2 * i + 1; // left = 2*i + 1
    var r = 2 * i + 2; // right = 2*i + 2
    
    // If left child is larger than root
    if (
      l < n &&
      Number(blocks[l].childNodes[0].innerHTML) >
        Number(blocks[largest].childNodes[0].innerHTML)
    )
      largest = l;
    
    // If right child is larger than largest so far
    if (
      r < n &&
      Number(blocks[r].childNodes[0].innerHTML) >
        Number(blocks[largest].childNodes[0].innerHTML)
    )
      largest = r;
    
    // If largest is not root
    if (largest != i) {
      var temp1 = blocks[i].style.height;
      var temp2 = blocks[i].childNodes[0].innerText;
      blocks[i].style.height = blocks[largest].style.height;
      blocks[largest].style.height = temp1;
      blocks[i].childNodes[0].innerText =
      blocks[largest].childNodes[0].innerText;
      blocks[largest].childNodes[0].innerText = temp2;
    
      await new Promise((resolve:any) =>
        setTimeout(() => {
          resolve();
        }, 250)
      );
    
      // Recursively Hapify the affected sub-tree
      await this.Heapify(n, largest);
    }
}
  
// Asynchronous HeapSort function
async HeapSort(n=this.datasetval.length) {
  var blocks:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(6) > div.card-body > section > div");
  // Build heap (rearrange array)
  for (var i = n / 2 - 1; i >= 0; i--) {
    await this.Heapify(n, i);
  }
  // One by one extract an element from heap
  for (var i = n - 1; i > 0; i--) {
  
    // Move current root to end
    var temp1 = blocks[i].style.height;
    var temp2 = blocks[i].childNodes[0].innerText;
    blocks[i].style.height = blocks[0].style.height;
    blocks[0].style.height = temp1;
    blocks[i].childNodes[0].innerText = 
    blocks[0].childNodes[0].innerText;
    blocks[0].childNodes[0].innerText = temp2;
  
    await new Promise((resolve:any) =>
      setTimeout(() => {
        resolve();
      }, 250)
    );
  
    // Call max Heapify on the reduced heap
    await this.Heapify(i, 0);
  }
}
    

  generatebars(num:number[]) {
        
        for (let i = 0; i < num.length; i++) {
          // To generate random values from 1 to 100
          const value = num[i];
          // To create element "div"
          const bar = document.createElement("div");
          // To add class "bar" to "div"
          bar.classList.add("bar");
          // Provide height to the bar
          bar.style.height = `${value * 3}px`;
          // Translate the bar towards positive X axis
          bar.style.transform = `translateX(${num[i] * 30}px)`;
          
          // To create element "label"
          let barLabel = document.createElement("label");

          // To add class "bar_id" to "label"
          barLabel.classList.add("bar_id");
          // Assign value to "label"
          barLabel.innerHTML = value.toString();
          
          // Append "Label" to "div"
          bar.appendChild(barLabel);
          // Append "div" to "data-container div"
          this.container.appendChild(bar);
        }
  }
   
}

 

</script>

<style scoped>
div.dataset,input{
  padding:2rem;
}
.data-container {
	width: 100%;
	height: 240px;
  position: relative;
  bottom: 10px;
}
.bar {
	width: 28px;
	position: absolute;
	left: 0;
	bottom: 0;
	background-color: rgb(0, 183, 255);
	transition: 0.2s all ease;
}

.bar_id {
	position: absolute;
	top: -30px;
	width: 100%;
	text-align: center;
}

.container{
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.dataset{
  display: flex;
  flex-direction: row;
  padding: 1;
}
input{
  flex:4;
  border: 1px solid #000;
  border-radius: 5px;
}
input:focus{
}
button{
  flex:1;

}
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  /* align-items: flex-start; */
}

.card {
  --padding: 3rem;
  background: white;
  border: 1px solid #777;
  border-radius: .25rem;
  overflow: hidden;
}

.card.card-shadow {
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, .2);
}

.card-header {
  font-size: 1.5rem;
  padding: var(--padding);
  padding-bottom: 0;
  margin-bottom: .5rem;
}

.card-header.card-image {
  padding: 0;
  overflow: hidden;
}

.card-header.card-image > img {
  display: block;
  width: 100%;
  max-height: 200px;
  aspect-ratio: 16 / 9;
  object-fit: cover;
  object-position: center;
  transition: 200ms transform ease-in-out;
}

.card:hover > .card-header.card-image > img {
  transform: scale(1.025);
}

.card-body {
  font-size: .9rem;
  padding: 0 var(--padding);
  padding-bottom: 20px;
  padding-top: 50px;
  align-items: center;
  justify-content: center;
}
.card-body >textarea{
  border: 1px solid black;
}
.card-footer {
  margin-top: 1rem;
  padding: var(--padding);
  padding-top: 0;
}

.btn {
  --color: hsl(200, 50%, 50%);
  background: var(--color);
  color: white;
  border: none;
  font-size: 1rem;
  padding: .5em .75em;
  cursor: pointer;
}

.btn.btn-outline {
  background: none;
  border-left: none ;
  color: #000;
}

.btn.btn-outline:hover, .btn.btn-outline:focus {
  background: #000;
  color:#fff;
}
/* For Sorting Designs */

</style>
