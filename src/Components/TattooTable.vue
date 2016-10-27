<template>
    <div class="box-body table-responsive">
        <div class="pull-right">
            <div class="box-body">
                <button type="button" class="btn btn-info margin" data-toggle="modal" data-target="#myModal" v-on:click="createGroup">{{createGroupLabel}}</button>
                <button type="button" class="btn bg-orange btn-flat margin">Total: {{total}} €</button>
            </div>

        </div>
        <table id="tattoo_table" class="table table-bordered table-striped">
            <thead>
            <tr>
                <th></th>
                <th>{{groupLabel}}</th>
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
                <td><input :checked="amIChecked(item.id)" type="checkbox" v-on:click="changeSeleted(item.id,item.price)"></td>
                <td v-if="item.group">{{item.group.name}}</td><td v-else></td>
                <td>{{item.name}}</td>
                <td>{{item.price}}</td>
                <td>{{item.feedback}}</td>
                <td>{{item.drawing}}</td>
                <td>{{item.photo}}</td>
                <td>{{item.client}}</td>
                <td>{{item.date}}</td>
            </tr>
            </tbody>
            <tfoot>
            <tr>
                <th></th>
                <th>{{groupLabel}}</th>
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
        <div class="modal fade" id="myModal" tabindex="-1" role="dialog">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                        <h4 class="modal-title">{{modalTitle}}</h4>
                    </div>
                    <div class="modal-body">
                        <div class="box-body">
                            <div class="span6 pull-right" style="text-align:right">
                                <p>Total: {{total}} €</p>
                            </div>
                            <div class="span6 pull-left" style="text-align:right">
                                <p>{{invoiceAmountLabel}}: {{selected.length}}</p>
                            </div>
                            <br><hr>
                            <div class="center-block">
                                <input class="form-control" :placeholder="enterGroupName" type="text" v-model="groupName">
                            </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save changes</button>
                    </div>
                </div><!-- /.modal-content -->
            </div><!-- /.modal-dialog -->
        </div><!-- /.modal -->
    </div>
</template>

<script>
    export default {
        props:{
            groupLabel:{},
            tattooReference:{},
            price:{},
            feedback:{},
            drawing:{},
            photo:{},
            client: {},
            date:{},
            previousLabel:{},
            nextLabel:{},
            createGroupLabel:{},
            invoiceAmountLabel:{},
            enterGroupName:{},
            modalTitle:{}
        },
        data: function () {
            return {
                items:null,
                total:0,
                selected:[],
                groupName:'',
                modalBody:'',
                groupName:'',
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
            createGroup(){
                var data = {groupName:this.groupName,ids:this.selected};
                this.modalBody = this.createModalTemplate();
                console.log(data);
//                this.$http.post('api/v1/group',data).then(function (response) {
//
//                }, function () {
//
//                });
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