<template>
  <div id="app">
    <v-container fluid>
      <b-jumbotron bg-variant="info" text-variant="white" border-variant="dark" >

       <template slot="header">
         Catclicker App
       </template>
       
       <template slot="lead">
         Welcome to the Catclicker App
       </template>

</b-jumbotron>

<b-row>

<b-col lg="4">

<div class="navigation">
  <b-list-group>
  <b-list-group-item v-for="[index,cat] in list" variant="info" @click="activate(index,cat)" :class="{active:isActive(cat)}" >{{cat.CatName}} <b-badge variant="light">{{cat.CatClicks}}</b-badge></b-list-group-item>
</b-list-group>
</div>


</b-col>

<b-col lg="4">

<div class="align-middle justify-content-center  " >
  <b-card :header="active.item.CatName" 
          :img-src="active.item.CatImage"
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2 w-100 rounded justify-content-center ">
    <p class="card-text">
    aka {{active.item.CatNickNames}}
    </p>
 
  </b-card>
</div>

</b-col>

<b-col lg="4">

<div class="form  ">
     <b-form @submit="onSubmit" @reset="onReset" v-show="show">
      <b-form-group id="exampleInputGroup1"
                    label="Cat Name "
                    label-for="Catname"
                    description="We'll never share your email with anyone else.">
        <b-form-input id="Catname"
                      type="email"
                      v-model="form.name"
                      required
                      :placeholder="holder.CatName">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup2"
                    label="Clicks "
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="text"
                      v-model="form.clicks"
                      required
                      :placeholder="String(holder.CatClicks)">
        </b-form-input>
      </b-form-group>
    
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
</div>

</b-col>


</b-row>

<hr class="my-4">
<v-container>
<div class="galary">
<h2>Galary</h2>
  <b-row>
<b-col lg="3" v-for="galary in CatData">
  <b-card :img-src="galary.CatImage"
                img-alt="Card image"
                img-top
                :class="{'fixed-height':true,'border-primary':isActive(galary) ,rounded:true }"
                >
            <p class="card-text p-3 mb-2 bg-dark text-white">
               {{galary.CatName}}
            </p>
        </b-card>
</b-col>
  </b-row>

</div>
</v-container>

    </v-container>
  </div>
</template>

<script>

import CatData from './assets/catData.json';

export default {
  name: 'app',
  watch:{
    active:function(newValue){
      console.log(newValue);
      this.form.name=newValue.item.CatName;
      this.form.clicks=newValue.item.CatClicks;
      console.log(this.form);
    }
  },
  methods:{
        
    activate(index,val){
      this.active.index=index;
      this.active.item=val;
        },
    isActive(val){
      if(val.CatName===this.active.item.CatName)
      {
        console.log(val.CatName);
          return true;
      }
    
      return false;
    },
    onSubmit (evt) {
      evt.preventDefault();
   console.log(evt);
   
    },
    onReset (evt) {
      evt.preventDefault();
      /* Reset our form values */
      this.form.clicks = '';
      this.form.name = '';
 
      /* Trick to reset/clear native browser form validation state */
      this.show = false;
      this.$nextTick(() => { this.show = true });
    }
  },
  data () {
    return {
      CatData,
      active:{
        index:0,
        item:CatData[0]
        },
      name: '',
      show:true,
      form:{
        name:"",
        clicks:"",

      },
      list:Object.entries(CatData)
    }
    
  },
   computed: {
     holder(){
       return this.active.item;
     },
    state () {
      return this.name.length >= 4 ? true : false
    },
    invalidFeedback () {
      if (this.name.length > 4) {
        return ''
      } else if (this.name.length > 0) {
        return 'Enter at least 4 characters'
      } else {
        return 'Please enter something'
      }
    },
    validFeedback () {
      return this.state === true ? 'Thank you' : ''
    }
  },
}
</script>

<style lang="scss">

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.align-center{
  margin:0px auto;
  padding:0px auto;
}
.form{
  text-align:left;
}
.navigation{
  height:70vh;
  overflow:scroll;
}
.card.fixed-height{
  img{
    height:250px;
  }
  text-align:left;
  margin-bottom: 25px;
}
</style>
