<script >
  import {state} from '../state.js';
  import axios from 'axios'


  export default {
   

    data(){
        return{     
            state,
            arrProduct:[],
            arrCategory:[],
            categoryId: 0,
            
            catinput:0,
        }
    },
    methods:{
      getCategory(){

        axios
        .get(state.baseUrl + 'api/categories', {})
        .then(response => {
          this.arrCategory = response.data.results;
        });

      },
      changeCategory(value, n){
        if(value==1){
          this.getProduct(0)
          this.categoryId=value

          
        }else{
          this.getProduct(value)
          this.categoryId=value


        }
      },
      catopen(){
        if (this.catinput){
          this.catinput = 0
        }else{
          this.catinput = 1
        }
        console.log(this.catinput)
      },
      getProduct(cat){
        this.categoryId = cat,
        axios
				.get(state.baseUrl + 'api/projects', {
					params: {
						category: this.categoryId,
					},
				})
				.then(response => {
          this.arrProduct = response.data.results.data;
				});
      },

      getPrice(cent){
        let num = parseFloat(cent);
        num = num / 100;
        num = "€" + num  
        
        return num
      },
      fixtag(arr){
        let arrtag='';
        arr.forEach((element, i) => {
          
          if(i+1==arr.length){
            
            arrtag = arrtag + element.name + '.'
          }else{
            arrtag = arrtag + element.name + ', '
            
          }
        });
        return arrtag
      },
      
      
      
    },
    created(){
      this.getProduct(0);
      this.getCategory();


      this.state.actvPage = 2;
    },
    
  }
</script>

<template>
  <div class="menu">
    <div class="menu-cont">
      <div class="menu-left">
        <img src="../assets/img/crop.png" alt="" class="bac">
        
      </div>
      <div class="menu-right">
        <div class="menu-top">
          <div class="menu-top-left">
            <div class="menu-top-respo">
              <img src="../assets/img/crop.png" alt="" class="bac-respo">
              <h1>Menu</h1>
            </div>
            <p>Le delizie del nostro menu aspettano solo te...</p>
            
          </div>
          <div class="menu-top-right">
            <div class="one-category shadow" @click="catopen(catinput)" :class="catinput ? 'cat-off': 'cat-on'">
              <span >CATEGORIE</span>
            </div>
            <div class="categorie"   :class="catinput ? 'cat-on': 'cat-off'">
              <div v-for="(cat, i) in arrCategory" class="category" :class="categoryId == cat.id ? 'category-on' : '', i == 0 ? 'category0' : '',i == 1 ? 'category1' : '', i == 2 ? 'category2' : '',i == 3 ? 'category3' : '',i == 4 ? 'category4' : '',i == 5 ? 'category5' : '',i == 6 ? 'category6' : '',i == 7 ? 'category7' : '',i == 8 ? 'category8' : '' ,i == 9 ? 'category9' : '',i == 10 ? 'category10' : '',i == 11 ? 'category11' : '',i == 12 ? 'category12' : '',i == 13 ? 'category13' : '',i == 14 ? 'category14' : '',i == 15 ? 'category15' : '',i == 16 ? 'category16' : '',i == 17 ? 'category17' : '',i == 18 ? 'category18' : '',i == 19 ? 'category19' : '',i == 20 ? 'category20' : '',i == 21 ? 'category21' : '',i == 22 ? 'category22' : '',i == 23 ? 'category23' : '',i == 24 ? 'category24' : '',i == 25 ? 'category25' : '',i == 26 ? 'category26' : '',i == 27 ? 'category27' : '',i == 28 ? 'category28' : '',i == 29 ? 'category29' : ''" @click="changeCategory(cat.id, cat.name)" :key="i"> 
                <span @click="catopen(catinput)" :class="categoryId == cat.id ? 'span-on' : '' ">{{ cat.name }}</span> 
              </div>
            </div>
          </div>
        </div>
  
       
        <div class="menu-bottom">

          <div class="card " v-for="item in arrProduct">
            <img  class="shadow" src="../assets/img/imgsushi.png" alt="">         <!--state.getImageUrl(item.image)-->
            <div class="c-tp shadow">
              <div class="title">{{ item.name }}</div>
              <div class="tags"> <span>{{fixtag(item.tags) }}</span></div>
              <div class="price">{{ getPrice(item.price) }}</div>
              <div class="allerg">
                <div class="allergs"></div>
                <div class="allergs"></div>
                <div class="allergs"></div>
                <div class="allergs"></div>
              </div>
            </div>
          </div>
          
        </div>

      </div>
    </div>
    
  </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;


.categorie::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.categorie::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.categorie::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.categorie::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}
.menu-cont::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.menu-cont::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.menu-cont::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.menu-cont::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}
.hd{box-shadow: 10px 10px 10px black; }

.menu{
  width: 100%;
  overflow: hidden;
  display: flex;
  flex-direction:column;
  position: fixed;
  top: 0;
  left: 0;
  flex-wrap: wrap;
  height: 100vh;
  margin-top: 230px;
  
  .menu-cont{
    overflow: auto;
    display: flex;
    background-color: $c-background;
    width: 100%;
    padding: 1rem 1rem ;
    padding-bottom: 250px!important;
    overflow-x: hidden;
    .menu-left{
      width: 10%;
      display: flex;
      align-items: center;
      position: relative;
      
      .bac{
        width: 100%;
        margin: auto;
      }
      
    }

    .menu-right{
      width: 90%;
      .menu-top{
        
        display: flex;
        justify-content: space-between;
        h1{
          font-size: 50px!important;
          padding-top: 2rem;
        }
        p{
          font-size: 20px;
         
        }

        img{
          display: none;
        }
        
      }
      .menu-bottom{
      @include dfc;
      flex-wrap: wrap;
      gap: 0rem;
      align-items: stretch;
      padding-bottom: 300px;
      .card{
        border-radius: 10px;
        width: calc((75% - 2rem) / 3);
        padding: 10px;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin: 15rem 1rem;
        margin-bottom:0 ;
        
        
        img{
          position: absolute;
          top: -130px;
          left: 0;
          right: 0;
          margin: auto;
          width: 250px;
          
          
        }
        .title{
          font-size: 20px;
          width: 100% ;
          text-transform: uppercase;
          z-index: 10001;
          
          
        }
        .c-tp{
          background-color: #AB2F2F;
          position: relative;
          z-index: 10000;
          display: flex;
          flex-direction: column;
          padding: 1rem 1.5rem;
          border-radius: 20px;
          justify-content: space-between;

          .tags, .price{
            border-radius: 10px;
            width: 100%;
            padding-bottom: .5rem;
          }
          .tags{

            display: flex;
            padding-top: 1rem;
            padding-right: .5rem;
            span{
              font-size: 13px;
              font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
              font-weight: bold!important; 


            }
          }
          .price{
            width: 100%;
            //border-radius: 10px ;
            text-align: right;
            padding-top: 0.5rem;
          }
          .allerg{
            position: absolute;
            bottom: -15px;
            width: 50%;
            display: flex;
            gap: 1rem;
            .allergs{
              width: 30px;
              aspect-ratio: 1;
              background-color: white;
              border-radius: 50%;
            }
          }
        }
      }
      }
    }
    
 

  }


}

/*** */
.one-category{
  background-color: #523333;
  width: 350px;
  
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  padding: 1.5em 1em;
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 50px;
  margin: 40px ;
  span{
    font-size: 30px;
    
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    
    letter-spacing: .1em;
  }
}
.categorie {
  box-shadow: -40px 50px 100px black ;
  background-color: #523333;
  max-width: 600px;
  width: 90%;
  height: 300px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  gap: 5px;
  padding: 1.5em 1em;
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 20px;
  overflow: hidden;
  overflow-y: auto;
  .category {
   height: 100%;
   flex: 1;
   
   cursor:grab;
   border-radius: 2px;
   transition: all .5s;
   background-color: #D53C3C;
   display: flex;
   justify-content: center;
   align-items: center;
   span {
    min-width: 30em;
    padding: .5em;
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    color: $c-nav-link;
    letter-spacing: .1em;
   }
  }

.category0{
  background-color:rgba(213, 60, 60, 0.64);
}
.category1{
  background-color:rgba(213, 60, 60, 0.62);
}
.category2{
  background-color:rgba(213, 60, 60, 0.60);
}
.category3{
  background-color:rgba(213, 60, 60, 0.58);
}
.category4{
  background-color:rgba(213, 60, 60, 0.56);
}
.category5{
  background-color:rgba(213, 60, 60, 0.54);
}
.category6{
  background-color:rgba(213, 60, 60, 0.52);
}
.category7{
  background-color:rgba(213, 60, 60, 0.50);
}
.category8{
  background-color:rgba(213, 60, 60, 0.48);
}
.category9{
  background-color:rgba(213, 60, 60, 0.46);
}
.category10{
  background-color:rgba(213, 60, 60, 0.44);
}
.category11{
  background-color:rgba(213, 60, 60, 0.42);
}
.category12{
  background-color:rgba(213, 60, 60, 0.40);
}
.category13{
  background-color:rgba(213, 60, 60, 0.38);
}
.category14{
  background-color:rgba(213, 60, 60, 0.36);
}
.category15{
  background-color:rgba(213, 60, 60, 0.34);
}
.category16{
  background-color:rgba(213, 60, 60, 0.32);
}
.category17{
  background-color:rgba(213, 60, 60, 0.30);
}
.category18{
  background-color:rgba(213, 60, 60, 0.28);
}
.category19{
  background-color:rgba(213, 60, 60, 0.26);
}
.category20{
  background-color:rgba(213, 60, 60, 0.24);
}
.category21{
  background-color:rgba(213, 60, 60, 0.22);
}
.category22{
  background-color:rgba(213, 60, 60, 0.20);
}
.category23{
  background-color:rgba(213, 60, 60, 0.18);
}
.category24{
  background-color:rgba(213, 60, 60, 0.16);
}
.category25{
  background-color:rgba(213, 60, 60, 0.16);
}
.category26{
  background-color:rgba(213, 60, 60, 0.14);
}
.category27{
  background-color:rgba(213, 60, 60, 0.12);
}
.category28{
  background-color:rgba(213, 60, 60, 0.10);
}
.category-on {
  
  background-color: rgba(213, 60, 60,);
}
  .category:hover {
    
  }
  .category:hover span {
    color: white;
   transform: rotate(0);
  }
}

.category-on:hover {
  
  background-color: $c-header !important;
}
.span-on{
  color: white!important;;

}

.cat-off{display: none;}

/***** */



@media (max-width:$bp1) {
  .menu{
    width:100%;
  }
}
@media (max-width:1600px) {
  .card{
    width: calc((75% - 2rem) / 2)!important;
  }
}

@media (max-width: 1300px){
  .menu{
    margin-top:150px!important;
  }
}
@media (max-width:1100px) {
  
  .card{
    width: calc((100% - 2rem) / 2)!important;
  }
  .menu-cont{
    padding-top: 0!important;
  }
    .menu-top{
      flex-direction: column;
      align-items: center;
      .menu-top-left{
        padding: 2rem;
        padding-top: 0;
        
        h1{
          padding-top: 0!important;
          
        }
        
        .menu-top-respo{
          display: flex;
          align-items: center;
          justify-content: space-between;
          width: 80%;
          margin: auto;
        }
      }
    }
    
    
    .bac-respo{
      display: block!important;
      width: 100px;
      transform: rotateZ(120deg);
    }
    
    .card{
    margin-top: 200px!important;
    width: 55% !important;
  }
  .menu-left{
    display: none!important;
  }
  .menu-right{
    width: 100%!important;
  }
}

@media (max-width:$bp2) {
  .menu-top-left{
    width: 100%;
    display: flex;
    flex-direction: column;
    .menu-top-respo{
      width: 100%!important;
      display: flex;
      justify-content: space-between;
      h1{
        font-size: 40px!important;
        
      }
  
      .bac-respo{
        width: 70px!important;
      }
    }
  }
  .menu-cont{
    width: 100%!important;
  }

  .card{
    
    width: 95% !important;
  }
}
@media (max-width:450px) {
  .menu-top-left{
    
    .menu-top-respo{
      padding-top: 3rem;
      text-align: center;
      
      
      h1{
        font-size: 40px!important;
      }
      .bac-respo{
        margin-right: 25px!important;
        width: 60px!important;
      }
      
    }
  }
  .one-category{
    width: 300px!important;
  }
  .categorie{
    max-width: 350px;
  }
  
}
</style>
