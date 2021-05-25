<template>
  <li>
    <h2>{{ name }} {{isFavrt ? '(👍)' : '(👎)' }}</h2>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button> 
    <button @click="toggleFavrt">{{ isFavrt ? 'Dislike👎' : 'Like👍' }} </button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  //use this or : props : simple

  // props:[
  //   'name',
  //   'phoneNumber',
  //   'emailAddress'
  // ],

  //like this : props as validator
  props:{
    id:{
      type:String,
      required: true
    },
    name:{
      type:String,
      required:true,
      default:"Arjun Sachin Tendulkar"
    },
    phoneNumber:String,
    emailAddress:String,
    isFavrt:Boolean
  }, 
 // emits:['toggle-favrt-inParent'],   //write direct or as object
 emit:{
   'toggle-favrt-inParent': function(id){
     if(id){
       return true;
     }
     else{
       console.log("ID not sending while emiting");
     }
   }
 },

  data() {
    return {
      detailsAreVisible: false,
      localIsFavrt: this.isFavrt
      // friend: {
      //   id: "manuel",
      //   name: "Manuel Lorenz",
      //   phone: "0123 45678 90",
      //   email: "manuel@localhost.com",
      // },
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavrt(){
      // this.localIsFavrt= !this.localIsFavrt
      this.$emit('toggle-favrt-inParent', this.id)
    }
  }
};
</script>

<style scoped>
button{
  margin: .5rem;
}
</style>