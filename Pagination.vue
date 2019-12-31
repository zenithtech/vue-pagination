<template>
    <div class="container">
        <div class="row w-100 m-0">
            <div class="col col-12 d-block text-center p-0 py-5 pagination">
                <template v-if="pagination_data.current_page === 1">
                    <span class="prev page-numbers disabled" aria-disabled="true"><i class="fa fa-caret-left"></i></span>
                </template>
                <template v-else>
                    <a class="prev page-numbers" v-on:click.prevent="goto(pagination_data.current_page - 1)"><i class="fa fa-caret-left"></i></a>
                </template>

                <template v-for="n in pagination_data.last_page">
                    <template v-if="pagination_data.current_page === n">
                        <a class="page-numbers current" v-html="n"></a>
                    </template>
                    <template v-else>
                        <template v-if="((
                                        (n < (pagination_data.current_page + 3) && n <= 6 && (pagination_data.current_page <= 4)) || (n > (pagination_data.last_page - 1))
                                        ) || (
                                        (n > (pagination_data.current_page - 3) && n > (pagination_data.last_page - 6) && (pagination_data.current_page > (pagination_data.last_page - 4))) || (n === 1)
                                        )) || (
                                            (n > (pagination_data.current_page - 3)) && n < (pagination_data.current_page + 3)
                                        )
                                        ">
                            <a class="page-numbers" v-on:click.prevent="goto(n)" v-html="n"></a>
                        </template>
                        <template v-else>
                            <template v-if="(n === (pagination_data.current_page - 3)) || n === (pagination_data.current_page + 3)">
                                <span class="page-numbers dots">…</span>
                            </template>
                        </template>
                    </template>
                </template>

                <template v-if="pagination_data.current_page < pagination_data.last_page">
                    <a class="next page-numbers" v-on:click.prevent="goto(pagination_data.current_page + 1)"><i class="fa fa-caret-right"></i></a>
                </template>
                <template v-else>
                    <span class="next page-numbers disabled" aria-disabled="true"><i class="fa fa-caret-right"></i></span>
                </template>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'pagination',
        props: [
            'pagination_data',
            'pagination_goto'
        ],
        watch: {
            pagination_data: function(){
                if(typeof this.pagination_data.current_page === 'number'){
                    this.$emit('update:pagination_goto', this.pagination_data.current_page);
                } else {
                    this.$emit('update:pagination_goto', false);
                }
            }
        },
        methods: {
            goto(page){
                this.$emit('update:pagination_goto', page);
            }
        }
    }
</script>
