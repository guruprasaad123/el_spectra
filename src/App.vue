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

<div class="align-middle justify-content-center " >
  <b-card :header="active.item.CatName" 
          :img-src="active.item.CatImage"
          img-alt="Image"
          img-top
          @click="clicked"
          tag="article"
          style="max-width: 20rem;"
          class="mb-2 w-100 rounded justify-content-center  bg-dark text-white">
    <p class="card-text ">
    aka {{active.item.CatNickNames}}<br>
    {{age(active.item)}}
    </p>
 
  </b-card>
</div>

</b-col>

<b-col lg="4">

  <div class="d-block p-2 bg-dark text-white">
      <p class="lead">Want a new Cat?</p>
<b-button variant="success" @click="modal_cat=true">New Cat</b-button>
  </div>

<div class="form  ">
     <b-form @submit="onSubmit" @reset="onReset" v-show="show">
      <b-form-group id="exampleInputGroup1"
                    label="Cat Name "
                    label-for="Catname"
                    description="Enter a kitty name">
        <b-form-input id="Catname"
                      type="text"
                      v-model="form.name"
                      required
                      :placeholder="holder.CatName">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup2"
                    label="Clicks "
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="number"
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
<h2>Cat Image Galary</h2>
  <b-row>
<b-col   lg="3" v-for="[index,galary] in list">
  <b-card :img-src="galary.CatImage"
                img-alt="Card image"
                img-top
                @click="activate(index,galary)"
                :class="{'fixed-height':true,'border-primary':isActive(galary) ,rounded:true }"
                >
            <p  :class="{'card-text':true,'p-3':true, 'mb-2':true, 
             'bg-dark':isActive(galary),'text-white':isActive(galary)}">
               {{galary.CatName}}<br>
               No.of times Clicked : {{galary.CatClicks}}<br>
               {{age(galary)}}
            </p>
        </b-card>
</b-col>
  </b-row>

</div>
</v-container>

    </v-container>
  
  
  <b-modal v-model="modal_cat" hide-footer title="New Entry" >
 <div class="form">
    <b-form  @reset="modal_reset" v-if="show">

      <b-form-group id="exampleInputGroup1"
                    label="Kitten Name"
                    label-for="exampleInput1"
                    description="Enter the Kitty Name">
        <b-form-input id="exampleInput1"
                      type="text"
                      v-model="modal_form.name"
                      required
                      placeholder="Enter CatName">
        </b-form-input>
      </b-form-group>

      <b-form-group id="exampleInputGroup2"
                    label="Nick Name :"
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="text"
                      v-model="modal_form.nickname"
                      required
                      placeholder="Nicky">
        </b-form-input>
      </b-form-group>

      <b-form-group id="exampleInputGroup3"
                    label="Image url "
                    label-for="exampleInput3">
        <b-form-input id="exampleInput3"
                      type="url"
                      v-model="modal_form.url"
                      required
                      placeholder="http://">
        </b-form-input>
      </b-form-group>

    <b-button @click="modal_submit"  variant="primary">Create</b-button>
   <b-button  type="reset" variant="danger">Reset</b-button>

    </b-form>


  </div>
  </b-modal>
  
  
  </div>
</template>

<script>

import CatData from './assets/catData.json';

export default {
  name: 'app',
  watch:{
    active:function(newValue){
     this.age(newValue.item);
    },
    catAge:function(newValue){

      this.active.item.catAge=newValue;
      this.list[this.active.index].CatAge=newValue;

    }
  },
  methods:{
    age(val){
      
      return ((val.CatClicks>=0 && val.CatClicks<=5)?"Infant":
             (val.CatClicks>=6 && val.CatClicks<=12)?"Child":
             (val.CatClicks>=13 && val.CatClicks<=25)?"Young":
             (val.CatClicks>=26 && val.CatClicks<=40)?"Middle-Age":
             (val.CatClicks>=41 && val.CatClicks<=60)?"Old":"Very-Old");
    },
    modal_submit(){
      let data={
    CatName:this.modal_form.name,
    CatClicks:0, 
    CatAge:0,
    CatImage:this.modal_form.url ,
    CatNickNames:this.modal_form.nickname
};
      this.list.unshift(data);
      this.CatData.unshift(data);
    }
    ,modal_reset(){
      this.modal_form.name="";
      this.modal_form.clicks=0;
      this.modal_form.url="";
      this.modal_form.nickname="";
      this.modal_form.age=0;
    
    },
        clicked(){
         let cur=this.active.item.CatClicks++;
         this.list[this.active.index].CatClicks=cur;
        },
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
   
   let name=this.active.item.CatName=this.form.name;
   this.list[this.active.index].CatName=name;

   let clicks = this.active.item.CatClicks= this.form.clicks;
   this.list[this.active.index].CatClicks=clicks;
   
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
        catAge:0,
      name: '',
      show:true,
      modal_cat:false,
      form:{
        name:"",
        clicks:"",
      },
      modal_form:{
        name:"",
        clicks:0,
        url:"",
        nickname:"",
        age:0,
      },
      
    }
    
  },
   computed: {
     list(){
     return Object.entries(this.CatData);
     },
     holder(){
       return this.active.item;
     },
     updatedAge(){
       this.catAge=this.age(this.active.item);
       return this.age(this.active.item);
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
