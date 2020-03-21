<template>
    <div>
        <el-table
                :data="tableData"
                border
                style="width: 100%">
            <el-table-column
                    fixed
                    prop="id"
                    label="编号"
                    width="150">
            </el-table-column>
            <el-table-column
                    prop="name"
                    label="图书名"
                    width="120">
            </el-table-column>
            <el-table-column
                    prop="author"
                    label="作者"
                    width="120">
            </el-table-column>

            <el-table-column
                    fixed="right"
                    label="操作">
                <template slot-scope="scope">
                    <el-button @click="edit(scope.row)" type="text" size="small">修改</el-button>
                    <el-button @click="deleteBook(scope.row)" type="text" size="small">删除</el-button>
                </template>
            </el-table-column>
        </el-table>

        <el-pagination
                background
                layout="prev, pager, next"
                :page-size= "pageSize"
                :total= "total"
                @current-change="page">
        </el-pagination>
    </div>
</template>

<script>
    export default {
        methods: {
            edit(row) {
                this.$router.push({
                    path: '/update',
                    query:{
                        id:row.id,
                    }
                })
                // this.$router.push('/update')
                // console.log(row);
                // console.log(row.id);
            },
            deleteBook(row){
                const _this = this
                axios.delete('http://localhost:8181/book/deleteById/'+row.id).then(function (resp) {
                    _this.$alert('《' + row.name + '》删除成功!', 'OK', {
                        confirmButtonText: '确定',
                        callback: action => {
                            window.location.reload();
                        }
                    });
                })
            },
            page(currentPage) {
                const _this = this;
                axios.get('http://localhost:8181/book/findAll/'+(currentPage-1)+'/2').then(function(resp) {
                    _this.tableData = resp.data.content;
                    _this.pageSize = resp.data.size;
                    _this.total = resp.data.totalElements;

                    // switch (currentPage) {
                    //     case 1:
                    //         this.tableData = [{
                    //             id: 1,
                    //             name: '王小虎',
                    //             author: '上海'
                    //         }, {
                    //             id: 2,
                    //             name: '王小虎',
                    //             author: '上海'
                    //         }, {
                    //             id: 3,
                    //             name: '王小虎',
                    //             author: '上海',
                    //         }]
                    //         break;
                    //     case 2:
                    //         this.tableData = [{
                    //             id: 4,
                    //             name: '王小虎',
                    //             author: '上海'
                    //         }, {
                    //             id: 5,
                    //             name: '王小虎',
                    //             author: '上海'
                    //         }, {
                    //             id: 6,
                    //             name: '王小虎',
                    //             author: '上海',
                    //         }]
                    //         break;
                    // }
                })
            }
        },

        data() {
            return {
                pageSize: 0,
                total: 0,
                tableData: [{
                    id: 1,
                    name: '王小虎',
                    author: '上海'
                }, {
                    id: 2,
                    name: '王小虎',
                    author: '上海'
                }, {
                    id: 3,
                    name: '王小虎',
                    author: '上海',
                }]
            }
        },
        created() {
            const _this = this;
            axios.get('http://localhost:8181/book/findAll/0/2').then(function(resp){
                _this.tableData = resp.data.content;
                _this.pageSize = resp.data.size;
                _this.total = resp.data.totalElements;
                // console.log(resp);
            })
        }
    }
</script>
<style scoped>

</style>