<template>
      <div class="container-flid">
                <div class="row">
                        <div class="col-md-12">
                                <div class="row ">


                                        <div class="col-md-6 ">
                                                <div class="col-md-12  d-flex ">
                                                        <input @keydown.enter="addTodo" type="text" class="form-control ">
                                                        <button @click="addİtem"  class="btn btn-danger ">İçerik Ekle</button>
                                                </div>

                                                <ul class="list-group "  v-if="itemList.length > 0">
                                                  <li  :class="{'tamamlandı' : todo.completed ,  'tamamlanmadı': !todo.completed }" class="list-group-item d-flex justify-content-between align-items-center" v-for="(todo,index) in itemList "  :key="index">
                                                <div class="col-md-12 d-flex justify-content-between align-items-center">
                                                        <input @click="tamamla(todo)" class="form-check-input ms-2 " :id="`completed_checkbox_${todo.id}`"  type="checkbox" v-model="todo.completed">
                                                           <label   class="form-check-label" :for="`completed_checkbox_${todo.id}`">{{todo.text}} </label>
                                                          <button @click="removeİtem(todo)" class="btn btn-sm btn-danger">Sil</button>
                                                </div> 
                                        </li>
                                      
                                        <div class="col-md-12"> 
                                                <p class="text-success">Tamamlanmış İçerik Sayfa:{{completedİtemCount}}</p>
                                        </div>
                                                </ul>

                                                 <div v-else class="col-md-12 alert alert-warning d-flex justify-content-center" >
                                                         <p>İçerik Eklenmemiş !</p>
                                                  </div>
                                        </div>


                                        <div class="col-md-6 p-0">
                                               <div class="row">
                                                        <div class="col-md-12 bg-success">
                                                                <h2 class="text-center">Tamamlanmış İşlemler</h2>
                                                        </div>
                                                        <div class="col-md-12">
                                                                <ul class="list-group">
                                                                        <li v-for="(okey,index) in tamamlanan" :key="index" class="list-group-item ">{{okey.text}}</li>
                                                                </ul>
                                                        </div>
                                               </div>
                                        </div>

                              


                                </div>
                        </div>
                </div>
      </div>

      
</template>

<script>
export default {
        data(){
                return{
                        itemList:[
                              
                        ],
                        tamamlanan:[
                        
                        ]
                }
        },
        methods:{
                addTodo(event){
                        this.itemList.push(
                                 {
                                        id:new Date().getTime(),
                                        text:event.target.value,
                                        completed:false
                                 }
                        );
                        event.target.value=" "
                },
                removeİtem(todoitem){
                        this.itemList = this.itemList.filter(todo => todo!= todoitem) //Tıklanan element haricindekileri yeniden filtrele
                        this.tamamlanan = this.itemList.filter(todo => todo!= todoitem)
                },   
                tamamla(x){
                        if(x.completed===false){
                                this.tamamlanan.push(x)

                        }
                       
                }
        },
      computed:{
        completedİtemCount(){
                 return this.itemList.filter((t)=> t.completed).length;
        },
         UncompletedİtemCount(){
                return this.itemList.filter((t)=> !t.completed).length;
        },

      
      
      }
}
</script>

<style>
        .tamamlandı{
                background-color: yellowgreen;

        }  
        .tamamlanmadı{
                background-color: rgb(212, 104, 104);
        }
</style>