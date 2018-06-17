<template>
    <div class="yosan">
        <div class="yosan-header container">
            <div class="row at-row">
                <div class="col-sm-19 col-xs-24">
                    <span v-text="title" class="title" />
                </div>
                <div class="col-sm-5 col-xs-24 sum-price-col">
                    <span class="sum-price">{{ this.sumPrice }}</span>
                </div>
            </div>
        </div> 
        <div class="yosan-body container">
            <at-table :columns="columns" :data="rows" class="table"></at-table>

            <!-- Edit Modal -->
            <!-- <at-modal v-model="editModal" title="編集" :styles="{top: '20px'}">編集</at-modal> -->
        </div>
        <div class="yosan-footer">
            <div class="container">
                <div class="row at-row">
                    <div class="col-sm-18 col-xs-24">
                        <at-input v-model="inputTitle" placeholder="項目"></at-input>
                    </div>
                    <div class="col-sm-4 col-xs-24">
                        <at-input v-model="inputPrice" placeholder="金額（円）"></at-input>
                    </div>
                    <div class="col-sm-2 col-xs-24">
                        <at-button type="primary" @click="addRow">追加</at-button>
                    </div>
                </div>
            </div>
        </div> 
    </div> 
</template>

<script>
export default {
    name: 'yosan_view',
    data: function () {
        return {
            title: 'タイトルです',
            sum_yen: '30000',
            rows: [
                {title: '行きの電車（新宿→成田空港)1', price: 1},
                {title: '行きの電車（新宿→成田空港)2', price: 10},
                {title: '行きの電車（新宿→成田空港)3', price: 100},
                {title: '行きの電車（新宿→成田空港)4', price: 1000}
            ],
            columns: [
                {
                    title: '項目',
                    key: 'title'
                },
                {
                    title: '値段',
                    key: 'price'
                },
                {
                    title: '操作',
                    render: (h, params) => {
                        return h('AtButton', {
                            props: {
                                size: 'small',
                                type: 'error',
                                hollow: false
                            },
                            on: {
                                click: () => {
                                    this.deleteRow(params.item)
                                }
                            }
                        }, '削除')
                    }
                }
            ],
            inputTitle: '',
            inputPrice: ''
        }
    },
    methods: {
        deleteRow: function (row) {
            console.log(row.index)
            this.rows.splice(row.index, 1)
        },
        addRow: function() {
            let row = {title: this.inputTitle, price: this.inputPrice}
            this.rows.push(row)
            this.inputTitle = ''
            this.inputPrice = ''
        }
    },
    computed: {
        sumPrice: function() {
            let result = 0
            this.rows.forEach(function(v){
                result = result + parseInt(v.price)
            })
            return result
        }
    }
}
</script>

<style lang="scss" scoped>
.yosan {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 48px);
    padding: 0 15px;
    .yosan-header {
        flex-grow: 0;
        flex-shrink: 0;
        padding: 15px 0;
        .title {
            font-size: 30px;
            @media screen and (max-width:300px){
                text-align: center;
            }
        }
        .sum-price {
            font-size: 30px;
        }
        .sum-price-col{
            text-align: right;
            @media screen and (max-width:300px){
                text-align: center;
            }
        }
    }
    .yosan-body {
        flex-grow: 1;
        .table{
            height: calc(100vh - 200px);
            overflow-y: scroll;
        }
    }
    .yosan-footer {
        flex-grow: 0;
        flex-shrink: 0;
        border-top: 1px solid #e2ecf4;
        padding: 15px 0;
    }
}
</style>

