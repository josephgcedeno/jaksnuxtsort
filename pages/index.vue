<template>
  <div class="container">
    <div class="dataset">
      <input type="text" ref="inputval" value="" name="datasetval" placeholder="Input Dataset eg(5,2,3,44,22,33)">
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
  timeoutdelay:number = 1000;


  //datasetval:string ='846335478';
  datasetval:number[] =[44,7,12,33,22,66,21,20,14];

  // * * Methods
  btnClicked(){
      this.datasetval = []
      let inputval:any = this.$refs.inputval;
      let newdata:number[] = inputval.value.split(",");
      
      if(newdata.length==1){
        alert("Cannot be like this")
        return;
      }
      setTimeout(()=>{
        this.datasetval = inputval.value.split(",");
      
         setTimeout(this.callSortingFunc,2000);
      },1000);

  }
  callSortingFunc(){
    alert("Start Sorting")
    this.SelectionSort();
    this.BubbleSort();
    this.InsertionSort();
    this.HeapSort();
    this.QuickSort();
    this.MergeSort();
  }
  
  mounted():void{
     this.container = this.$refs.containerdiv;
     this.bubblesortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(2) > div.card-body > section");
     this.insertionsortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(3) > div.card-body > section");
     this.mergesortcontainer = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(4) > div.card-body > section");
     this.quicksort = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(5) > div.card-body > section");
     this.heapsort = document.querySelector("#app > div > div.container > div.card-grid > div:nth-child(6) > div.card-body > section");
     setTimeout(this.callSortingFunc,1000);
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
        }, this.timeoutdelay)
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
      }, this.timeoutdelay)
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
              }, this.timeoutdelay);
          });
      });
  }
  // Asynchronous BubbleSort function
  async BubbleSort(delay = this.timeoutdelay) {
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
                  .style.backgroundColor = "rgb(49, 226, 13)";
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
        }, this.timeoutdelay)
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
            }, this.timeoutdelay)
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
          }, this.timeoutdelay)
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
        }, this.timeoutdelay)
      );
    
      // Recursively Hapify the affected sub-tree
      await this.Heapify(n, largest);
    }
}
  
// Asynchronous HeapSort function
  async HeapSort(n:number=this.datasetval.length) {
    var blocks:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(6) > div.card-body > section > div");
    // Build heap (rearrange array)
    for (var i = Math.floor(n / 2 )- 1; i >= 0; i--) {
      await this.Heapify(n, i);
    }
    // One by one extract an element from heap
    for (var i = n - 1; i > 0; i--) {
    
      // Move current root to end
      var temp1 = blocks[i].style.height;
      var temp2 = blocks[i].childNodes[0].innerText;
      blocks[i].style.height = blocks[0].style.height;
      blocks[0].style.height = temp1;
      blocks[i].style.backgroundColor = "rgb(49, 226, 13)";
      blocks[0].style.backgroundColor = "rgb(49, 226, 13)";
      blocks[i].childNodes[0].innerText = 
      blocks[0].childNodes[0].innerText;
      blocks[0].childNodes[0].innerText = temp2;
    
      await new Promise((resolve:any) =>
        setTimeout(() => {
          resolve();
        }, this.timeoutdelay)
      );
    
      // Call max Heapify on the reduced heap
      await this.Heapify(i, 0);
    }
  }
  async lometo_partition(l:number, r:number, delay = this.timeoutdelay) {
    var blocks:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(5) > div.card-body > section > div");
    
    // Storing the value of pivot element
    var pivot = Number(blocks[r].childNodes[0].innerHTML);
    var i = l - 1;
    blocks[r].style.backgroundColor = "red";
    //document.getElementsByClassName("range")[0].innerText = ``;
    var range = [l,r]
    
    for (var j = l; j <= r - 1; j++) {
      // To change background-color of the
      // blocks to be compared
      //blocks[j].style.backgroundColor = "yellow";
      // To wait for 700 milliseconds
      await new Promise((resolve:any) =>
        setTimeout(() => {
          resolve();
        }, delay)
      );
      var value =  Number(blocks[j].childNodes[0].innerHTML);
    
      // To compare value of two blocks
      if (value < pivot) {
        i++;
        var temp1 = blocks[i].style.height;
        var temp2 = blocks[i].childNodes[0].innerText;
        blocks[i].style.height = blocks[j].style.height;
        blocks[j].style.height = temp1;
        blocks[i].childNodes[0].innerText =
        blocks[j].childNodes[0].innerText;
        blocks[j].childNodes[0].innerText = temp2;
        //blocks[i].style.backgroundColor = "orange";
        //if (i != j) blocks[j].style.backgroundColor = "pink";
        //To wait for 700 milliseconds
        await new Promise((resolve:any) =>
          setTimeout(() => {
            resolve();
          }, delay)
        );
      } else blocks[j].style.backgroundColor = "pink";
    }
    // Swapping the ith with pivot element
    i++;
    var temp1 = blocks[i].style.height;
    var temp2 = blocks[i].childNodes[0].innerText;
    blocks[i].style.height = blocks[r].style.height;
    blocks[r].style.height = temp1;
    blocks[i].childNodes[0].innerText =
    blocks[r].childNodes[0].innerText;
    blocks[r].childNodes[0].innerText = temp2;
    //blocks[r].style.backgroundColor = "pink";
    //blocks[i].style.backgroundColor = "green";
    
    // To wait for 2100 milliseconds
    await new Promise((resolve:any) =>
      setTimeout(() => {
        resolve();
      }, delay*3)
    );
    //document.getElementsByClassName("range")[0].innerText = "";
    range = [];
    for (var k = 0; k < blocks.length; k++) 
    blocks[k].style.backgroundColor = "rgb(49, 226, 13)";
    return i;
  }
    
  // Asynchronous QuickSort function
  async QuickSort(l=0, r=this.datasetval.length-1) {
    if (l < r) {
      // Storing the index of pivot element after partition
      var pivot_idx = await this.lometo_partition(l, r);
      // Recursively calling quicksort for left partition
      await this.QuickSort(l, pivot_idx - 1);
      // Recursively calling quicksort for right partition
      await this.QuickSort(pivot_idx + 1, r);
    }
  }
  async merge(arr:any, l:number, m:number, r:number)
  {
        
        var n1 = m - l + 1;
        var n2 = r - m;
     
        // Create temp arrays
        var L = new Array(n1); 
        var R = new Array(n2);
        // Copy data to temp arrays L[] and R[]
        for (var i = 0; i < n1; i++)
            L[i] ={ data: parseInt(arr[l + i].childNodes[0].innerText), index:l + i , height:arr[l + i].style.height }
        for (var j = 0; j < n2; j++)
            R[j] = {data:parseInt(arr[m + 1 + j].childNodes[0].innerText), index:m + 1 + j , height:arr[m + 1 + j].style.height }
            var delay = 250;
           // await this.sleep(delay);
    
        var i = 0;
    
        // Initial index of second subarray
        var j = 0;
    
        // Initial index of merged subarray
        var k = l;
    
        while (i < n1 && j < n2) {
            arr[k].style.backgroundColor= "rgb(49, 226, 13)";

            if (L[i].data <= R[j].data) {
         
                arr[k].childNodes[0].innerText = L[i].data;
                arr[k].style.height = L[i].height;
                //arr[L[i].index].style.height = heighttemp;
                i++;
            }
            else {
          
                arr[k].childNodes[0].innerText = R[j].data;
                arr[k].style.height = R[j].height;
                //arr[R[j].index].style.height = heighttemp;
                j++;
            }
            k++;
        }
    
        // Copy the remaining elements of
        // L[], if there are any
        while (i < n1) {
            arr[k].style.backgroundColor= "rgb(49, 226, 13)";

            arr[k].childNodes[0].innerText = L[i].data;
            arr[k].style.height= L[i].height;
            //arr[L[i].index].style.height= heighttemp;
            i++;
            k++;
        }
    
        // Copy the remaining elements of
        // R[], if there are any
        while (j < n2) {
            arr[k].style.backgroundColor= "rgb(49, 226, 13)";
            arr[k].childNodes[0].innerText = R[j].data;
            arr[k].style.height= R[j].data.height;
            j++;
            k++;
            
        }
        
      

    }
    sleep(ms:number) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
    
   async mergeSorting(arr:any,l:number, r:number){

        if(l>=r){
      
            return;//returns recursively
        }
    
        var m =Math.floor(l+ Number((r-l)/2));
        
        this.mergeSorting(arr,l,m);
        this.mergeSorting(arr,m+1,r);
        await new Promise((resolve:any) =>
          setTimeout(() => {
            resolve();
          }, this.timeoutdelay)
        );
        this.merge(arr,l,m,r);

        
    }
    
    MergeSort(){
        var bars:any = document.querySelectorAll("#app > div > div.container > div.card-grid > div:nth-child(4) > div.card-body > section > div");
        this.mergeSorting(bars, 0, bars.length - 1);
     
    }
 
}

 

</script>

<style scoped>
div.dataset,input{
  padding:2rem;
}
.data-container {
	height: 240px;
  position: relative;
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
  border-right: none;
}
input:focus{
  outline:none;
}
button{
  flex:1;

}
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
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
  padding: 10%;  
  overflow-x: auto;
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
  font-weight: bold;
}

.btn.btn-outline {
  background: none;
  border:1px solid #000;
  border-left: none ;
  color: #000;
}

.btn.btn-outline:hover, .btn.btn-outline:focus {
  background: #000;
  color:#fff;
}
/* For Sorting Designs */

</style>
