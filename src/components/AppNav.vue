<script>
import { state } from "../state.js";
import axios from 'axios'

export default {
  data() {
    return {
      state,
      asporto: false,
      tavoli: false,
      ferie : {
        status : false,
        from : '',
        to: ''
      }
    };
  },
  methods: {
    home(){
      this.$router.replace("/");
    }
  },
  async created(){
   let respo = await axios.get(this.state.baseUrl + 'api/setting') 
   let setting = respo.data.results
   this.asporto = setting[0].status
   this.tavoli = setting[1].status
   this.ferie.status = setting[2].status
   this.ferie.from = setting[2].from
   this.ferie.to = setting[2].to
   
   
   
   console.log(this.setting)  
  }
};
</script>

<template>
  
  <div class="nav">
    <div class="left-nav">
      <img @click="home" src="../assets/img/logo_kojo.jpg" alt="">
    </div>
    <div class="right-nav">
      <p v-if="ferie.status" class="ferie">Siamo chiusi per ferie dal {{ ferie.from }} al {{ ferie.to }}</p>
      <div class="nav1">
        <img src="../assets/img/punta1.png" alt="">
        <div class="right-nav1"></div>
      </div>
      <div class="nav2">
        <img src="../assets/img/punta2.png" alt="">
        <div class="menu">
          <router-link :to="{ name: 'home' }" :class="state.actvPage == 1 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
          <router-link :to="{ name: 'menu' }" :class="state.actvPage == 2 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
          <router-link :to="{ name: 'prenota' }" v-if="asporto" :class="state.actvPage == 5 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
          <a href="tel:+393451187723" v-if="tavoli" class="nav-link"  >Prenota tavolo</a>
          <!-- <router-link :to="{ name: 'prenotaServizio' }" :class="state.actvPage == 6 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(6)" >Prenota tavolo</router-link> -->
        </div>

      </div>
      <div class="nav3">
        <img src="../assets/img/punta3.png" alt="">
        <div class="right-nav3"></div>
      </div>
      <div class="nav4">
        <div class="left-nav4">
          <img src="../assets/img/puntacsleft.png" alt="">
          <router-link :to="{ name: 'chi-siamo' }" :class="state.actvPage == 3 ? 'active-link' : '' "  @click="state.updateActvPage(3)" class="chi-siamo" ><span>chi siamo?</span></router-link>
          <img src="../assets/img/puntacsright.png" alt="">
        </div>
        <div class="center-nav4">

        </div>
        <div class="right-nav4">
          <img src="../assets/img/puntac.png" alt="">
          <div class="contatti"><router-link :to="{ name: 'contatti' }" :class="state.actvPage == 4 ? 'active-link' : '' " class="nav-link" @click="state.updateActvPage(4)" >contatti</router-link></div>
        </div>
      </div>
    </div>
    <div class="nav-mb">
      <div class="t-mb"></div>
      <div class="btn-menu" @click="state.openside" :class="state.sideMenuValue? 'btn-off' : 'btn-on'">
        <div class="l1"></div>
        <div class="l2"></div>
        <div class="l1"></div>
      </div>
    </div>
  </div>
  <p v-if="ferie.status" class="ferie-mb">Siamo chiusi per ferie dal {{ ferie.from }} al {{ ferie.to }}</p>
  <div :class="state.sideMenuValue ? 'nav-mb-on' : 'nav-mb-off'">
    <div :class="state.sideMenuValue ? 'burger-close-on' : 'burger-close-off'" @click="state.openside">
      <div class="line"  :class="state.infomenu ?   'menu-off': 'active-link' "></div>
      <div class="line l1" :class="state.infomenu ?   'menu-off': 'active-link' "></div>
    </div>
    <div :class="state.sideMenuValue ? 'top-on' : 'top-off'">
      <router-link :to="{ name: 'home' }" :class="state.infomenu ?   'menu-off': '' " class="nav-link" @click="state.updateActvPage(1)" >home</router-link>
      <router-link :to="{ name: 'menu' }" :class="state.infomenu ? 'menu-off': '' " class="nav-link" @click="state.updateActvPage(2)" >menu</router-link>
      <router-link v-if="asporto" :to="{ name: 'prenota' }" :class="state.infomenu ? 'menu-off': '' " class="nav-link" @click="state.updateActvPage(5)" >Ordina d'Asporto</router-link>
      <a href="tel:+393451187723" v-if="tavoli" :class="state.infomenu ? 'menu-off': '' " class="nav-link"  >Prenota tavolo</a>
      <router-link :to="{ name: 'chi-siamo' }" :class="state.infomenu ? 'menu-off': '' " class="nav-link" @click="state.updateActvPage(3)" >chi siamo?</router-link>
      <router-link :to="{ name: 'contatti' }" :class="state.infomenu ? 'menu-off': '' " class="nav-link" @click="state.updateActvPage(4)" >contatti</router-link>
      <div class="nav-link info"  :class="state.infomenu ? 'info-on' : 'info-off'">
        <div :class="state.infomenu ? 'top-info-on' : 'top-info-off'" >
          <h4 @click="state.infoside">info</h4>
          <span  @click="state.infoside" :class="state.infomenu ? 'info-btn' : 'info-n'">+</span>
        </div>

        <div :class="state.infomenu ? 'main-info-on' : 'main-info-off'">

          <div class="sec-1">
            <h4>Dove puoi trovarci</h4>
            <p>Monsano</p>
          </div>

          <div class="sec-2">
            <h4>Orari d'apertura</h4>
            <div class="cont-giorni">
                <span>lunedì</span>
                <span>martedì</span>
                <span>mercoledì</span>
                <span>giovedì</span>
                <span>venerdì</span>
                <span>sabato</span>
                <span>domenica</span>
            </div>
            <div class="cont-orari">
              <span class="time" >12-15 - 19-23</span>
              <span class="time" >chiusi</span>
              <span class="time" >12-15 - 19-23</span>
              <span class="time" >12-15 - 19-23</span>
              <span class="time" >12-15 - 19-23</span>
              <span class="time" >12-15 - 19-23</span>
              <span class="time" >12-15 - 19-23</span>
            </div>
          </div>

        </div>

        <div :class="state.infomenu ? 'sec-3' : 'sec-3-off'" >
          Kojo sushi, PI: 02913470429, 
          <a href="https://www.iubenda.com/privacy-policy/89654778/cookie-policy" class="link" title="Cookie Policy ">Cookie Policy, </a>
          <a href="https://www.iubenda.com/privacy-policy/89654778" class="link" title="Privacy Policy "> Privacy Policy</a>
          , product by 
          <a href="https://future-plus.it">FUTURE +</a>
        </div>

      </div>
    </div>

  </div>
  
  

</template>




<style lang="scss" scoped>

  @use "../assets/styles/general.scss" as *;
  

.link{
  text-decoration: none;
  color: white;
}
.nav-link.info{
  .top-info-on{
    padding: 10px;
    width:100%;
    @include dfc;
    justify-content: space-between;
  }
  .top-info-off{
    @include dfc;
    
  }
}
.ferie{
  margin-right: 10px;
}
.ferie, .ferie-mb{
  color: red;
}
.ferie-mb{
  margin-left: 10px;
  display: none;
}

.info-btn{
transform: rotateZ(765deg);
font-size:40px;
padding:20px;
transition: all .2s linear;

}
.info-on{
height:100%;
background-color:$c-footer-nav;
width:100%;
display: flex;
flex-direction: column;
justify-content: space-between;
transition: all .2s linear;
}

.main-info-off{
display: none;
}
.main-info-on{
@include dfc;
flex-direction: column;
justify-content: space-between;
text-align:center;
gap: 25px;
.sec-1{

    @include dfj;
    flex-direction: column;
    gap: 10px;
    width: 100%;


    h4{
      font-size:20px;

    }
    p{
      font-size:16px;
    }
  }
.sec-2{
  @include dfj;
  flex-wrap: wrap;
  gap: .6rem;
  width: 100%;
  justify-content: space-around;
  h4{
    
    width: 100%;
    padding-bottom:20px;
    font-size: 20px;
  }
  .cont-giorni, .cont-orari{
    font-size: 15px;
    @include dfj;
    flex-direction: column;
    gap: .3rem;
    text-align: left;
    text-transform: uppercase;
    
    .time{
      text-align: center;
    }
  }

}

}
.sec-3{
background-color: rgba(0, 0, 0, 0.43);
font-size: 10px;
padding: 10px;
}
.sec-3-off{
display: none;
}


.menu-off{
display:none;
}




.nav-mb-on{
position: fixed;
top: 0;
left: 0;
z-index: 1000;
background-color: #270000;
width: 100%;
height: 100%;
transition: all .3s linear;
}
.burger-close-on{
transition: all 1s linear 2s;
position: absolute;
top: 8%;
right: 8%;
opacity: 1;
transform: rotateZ(0deg);
transition: display .3s linear;
transition: opacity 1s linear 2s;
transition: transform 1s linear 3s;
.line{
  background-color: white;
  height: 30px;
  width: 5px;
  transform: rotateZ(765deg);
  position: absolute;
}
.l1{
  transform: rotateZ(135deg)
}
}
.burger-close-off{
transform: rotateZ(500deg);

display: none;
opacity: 0;
transition: display .3s linear;
transition: opacity 1s linear 2s;
transition: transform 1s linear 3s;

}


.bottom-footer-on{
display: none;
}
.nav-mb-off{
position: fixed;
top: 0;
left: 0;
z-index: 10;
background-color: #270000;
width: 100%;
height: 0;
transition: all .2s linear;


}
.top-off{
display: none;
opacity: 0;
transition: display .3s linear;
transition: opacity 1s linear 2s;


}
.bottom-footer-off{
display: none;
}

.info-n{
  position: relative;
  z-index: 300;
}


.infoopen{
height:100%;
background-color:$c-footer-nav;
width:100%;
justify-content: space-between;
transition: all 1s linear;
}
.infoclose{
height: 0%;
}



.infosideopen{
  height: auto;
  text-align:center;
  .sec-1{
      @include dfj;
      flex-direction: column;
      gap: 1rem;
      width: 100%;
      padding-bottom: 100px;

      h4{
        font-size:30px;
        padding-bottom:10px;
      }
      p{
        font-size:25px;
      }
    }
    .sec-2{
      @include dfj;
      flex-wrap: wrap;
      gap: 1rem;
      width: 100%;
      justify-content: space-around;
      h4{
        
        width: 100%;
        padding-bottom:30px;
        font-size: 30px;
      }
      .cont-giorni, .cont-orari{
        font-size: 15px;
        @include dfj;
        flex-direction: column;
        gap: .5rem;
        text-align: left;
        text-transform: uppercase;
        
        .time{
          text-align: center;
        }
      }
      padding-bottom: 50px;
    }
    .sec-3{
      background-color: rgba(0, 0, 0, 0.43);
      font-size: 10px;
      padding: 10px;
    }
    
}
.topinfoclose{
  display:none;
}
.nav{
  overflow: hidden;
  background-color: white;
  display: flex;
  width: 100%;
  height: 230px;
  z-index: 100;
  box-shadow: 0px 5px 30px  black;
  .left-nav{
    padding-left: 150px;
    height: 100%;
    @include dfc;
    img{
      height: 80%;
    }
  }
  .right-nav{
    align-items: flex-end;
    display: flex;
    height: 100%;
    flex-direction: column;
    width: 100%;
    
    .nav1{
      display: flex;
      height: 56px;
      width: 90%;
      margin-bottom: 8px;
      animation: slidein 1.1s 1 ease-in-out;
      img{
        height: 100%;
      }
     

      .right-nav1{
        background-color: $c-nav;
        width: 100%;
      }
      
    }
    .nav2{
      margin-bottom: 8px;
      display: flex;
      height: 48px;
      width: 85%;
      animation: slidein2 1.3s 1 ease-in-out;
      
      img{
        height: 100%;
      }
      .menu{
        background-color: #712A2A;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 200px 0 100px;
        font-size: 20px;
        text-transform: uppercase;
        
      }
      
    }
    .nav3{
      display: flex;
      height: 40px;
      width: 86%;
      animation: slidein3 1.5s 1 ease-in-out;
      img{
        height: 100%;
      }
      .right-nav3{
        background-color: #523333;
        width: 100%;

      }
    }
    .nav4{
      text-transform: uppercase;
      display: flex;
      height: 70px;
      width: 85%;
      animation: slidein4 1.7s 1 ease-in-out;
      img{
        height: 100%;
      }
      
      .left-nav4{
        display: flex;
        .chi-siamo{
          @include dfc;
          font-size: 20px;
          color: white;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;          
          width: 200px;
        }
      }

      .center-nav4{
        background-color: #523333;
        width: 100%;
        height: 100%;
      }
      .right-nav4{
        display: flex;
        img{
          height: 100%;
        }
        .contatti{
          @include dfc;
          font-size: 20px;
          color: white;
          background-color: #270000;
          border-top: 8px solid white;          
          border-bottom: 8px solid white;         
          border-right: 8px solid white; 
          width: 200px;
        }
      }
    
    }
    .nav-link, span{
        animation: opacityt 1.3s 1 ease-in-out;
        

      }
      
      @keyframes opacityt {
        0%{
          opacity: 0;
        }
        90%{
          opacity: 0%;
        }
        100%{
          opacity: 100%;
        }
        
      }
  }

  .nav-mb{
    overflow: hidden;
    display: none;
    position: relative;
    z-index: 5315;
    background-color: #523333;
    width: 100%;
    height:115px;
    animation: slideinm 1 1s ease-in-out;
    @keyframes slideinm {
      from{
        margin-left: 100%;
        width: 0%;
      }
      to{
        margin-left: 0%;
        width: 100%;

      }
    }

    .t-mb{
    background: linear-gradient(60deg, #FFF 50%, #523333 50%);
    height: 100%;
    width: 30%;
    min-width: 80px;
    
  }
  .btn-menu{
    position: relative;
    right: 20px!important;
    z-index: 20;
    flex-direction: column;
    gap: .7rem;
    align-items: flex-end;
    display: flex;
    animation: slideinmm 1 1s ease-in-out;
    @keyframes slideinmm {
      0%{
          opacity: 0;
        }
        90%{
          opacity: 0%;
        }
        100%{
          opacity: 100%;
        }
    }
    .l1{
      width: 40px;
      height: 5px;
      border-radius: 20px;
      background-color: white;
      
    }
    .l2{
      width: 50px;
      height: 5px;
      border-radius: 20px;
      background-color: white;
     
    }
    
    
  }
    
    
  }
}

@keyframes slidein {
        from {
          margin-left: 100%;
          width: 0%;
        }

        to {
          margin-left: 0%;
          width: 90%;
        }
      }
@keyframes slidein2 {
        from {
          margin-left: 100%;
          width: 0%;
        }

        to {
          margin-left: 0%;
          width:85%;
        }
      }
@keyframes slidein3 {
        from {
          margin-left: 100%;
          width: 0%;
        }

        to {
          margin-left: 0%;
          width: 86%;
        }
      }
@keyframes slidein4 {
        from {
          margin-left: 100%;
          width:0%;
        }

        to {
          margin-left: 0%;
          width: 85%;
        }
      }
.top-on{
  @include dfc;
  height: 100%;
  justify-content: space-around;
  flex-direction: column;
  padding: 10%;
  opacity: 1 ;
  transition: display .3s linear 1s;
  transition: opacity 5s linear 2s;

  .nav-link{

    text-transform: uppercase;
    line-height: 2rem;
    color: white;
    font-family: 'Gabarito', cursive;
    font-size: 1.8rem;
  }

}



@media (max-width: 1500px) {

  .nav{
    .nav1{
      width: 91%!important;
    }
    .nav3{
      width: 86%!important;
    }
    .nav4{
      width: 84.5%!important;
    }

  }
  .menu{
    padding: 0 100px 0 100px!important;
  }
}
@media (max-width: 1350px) {
  .menu{
    padding: 0 50px 0 50px!important;
  }
}
@media (max-width: 1300px) {
  .nav{
    height: 125px;
    .right-nav{
      display: none;
    }
  }
  .ferie-mb{
    display: block;
  }
  .ferie{
    display: none;
  }
  .nav-mb{
    display: flex!important;
    @include dfc;
    justify-content: space-between;
  }
}

@media (max-width: 600px){
  .nav{
    
    .left-nav{
        padding-left:0px!important;
      
    }
  }
}
@media (max-width: 450px){
}
@media (max-width: 400px){
  
  .nav-mb{
   
    .btn-menu{
      right: 20px!important;
    }
  }
}

</style>
