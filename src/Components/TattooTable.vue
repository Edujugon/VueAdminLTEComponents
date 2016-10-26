<template>
    <div class="box-body table-responsive">
        <div class="pull-right">
            <expandable-collapse
                    heading="Total"
                    :body="total"
                    collapse=true
            ></expandable-collapse>
        </div>
        <table id="tattoo_table" class="table table-bordered table-striped">
            <thead>
            <tr>
                <th></th>
                <th>{{tattooReference}}</th>
                <th>{{price}}</th>
                <th>{{feedback}}</th>
                <th>{{drawing}}</th>
                <th>{{photo}}</th>
                <th>{{client}}</th>
                <th>{{date}}</th>
            </tr>
            </thead>
            <tbody>
            <template v-if="!items">
                <div>
                    <h3>No Records Yet!</h3>
                </div>
            </template>
            <tr v-else v-bind:class="{ info: amIChecked(item.id) }" v-for="item in items">
                <input type="hidden" :value="item.id">
                <td><input :checked="amIChecked(item.id)" type="checkbox" v-on:click="changeSeleted(item.id,item.precio)"></td>
                <td>{{item.nombre}}</td>
                <td>{{item.precio}}</td>
                <td>{{item.comentario}}</td>
                <td>{{item.dibujo}}</td>
                <td>{{item.foto}}</td>
                <td>{{item.cliente}}</td>
                <td>{{item.fecha}}</td>
            </tr>
            </tbody>
            <tfoot>
            <tr>
                <th></th>
                <th>{{tattooReference}}</th>
                <th>{{price}}</th>
                <th>{{feedback}}</th>
                <th>{{drawing}}</th>
                <th>{{photo}}</th>
                <th>{{client}}</th>
                <th>{{date}}</th>
            </tr>
            </tfoot>
        </table>
        <ul class="pager">
            <li class="previous" v-show="pagination.previous">
                <a class="page-scroll" v-on:click="fechRecords('previous')">{{previousLabel}}</a>
            </li>
            <li class="next" v-show="pagination.next">
                <a class="page-scroll" v-on:click="fechRecords('next')">{{nextLabel}}</a>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props:{
            tattooReference:{},
            price:{},
            feedback:{},
            drawing:{},
            photo:{},
            client: {},
            date:{},
            previousLabel:{},
            nextLabel:{}
        },
        data: function () {
            return {
                items:null,
                total:0,
                selected:[],
                pagination: {
                    page: 1,
                    previous: false,
                    next: false
                }
            }
        },
        computed:{
        },
        methods:{
            fechRecords: function (direction) {

                if (direction === 'previous'){
                    --this.pagination.page;
                }
                else if (direction === 'next'){
                    ++this.pagination.page;
                }

                this.$http.post('api/v1/tattoos?page='+ this.pagination.page).then(function(response){
                    if(response.data.data)
                        this.items =  response.data.data;
                        this.pagination.next = response.data.next_page_url;
                        this.pagination.previous = response.data.prev_page_url;
                }, function(response){
                    console.log(response);
                });
            },
            changeSeleted: function (id,price) {
                var index = this.selected.indexOf(id);
                if (index > -1) {
                    this.selected.splice(index, 1);
                    //Sum the new amount
                    this.total -= price;
                }else{
                    this.selected.push(id);
                    this.total += price;
                }

            },
            amIChecked: function (id) {
                if (this.selected.indexOf(id) != -1) return true;
            }


        },
        mounted() {
            console.log('Tattoo Table ready.');
            this.fechRecords();
        }
    }
</script>