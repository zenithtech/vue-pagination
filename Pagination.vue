<template>
    <div class="container">
        <div class="row w-100 m-0">
            <div class="col col-12 d-block text-center p-0 py-5 pagination">
                <span v-if="pagination_data.current_page === 1" class="prev page-numbers disabled" aria-disabled="true"><i class="fa fa-caret-left"></i></span>
                <a v-else class="prev page-numbers" v-on:click.prevent="goto(pagination_data.current_page - 1)"><i class="fa fa-caret-left"></i></a>

                <template v-for="n in pagination_data.last_page">
                    <a v-if="pagination_data.current_page === n" class="page-numbers current" v-html="n"></a>
                    <template v-else>
                        <a v-if="(
                                (
                                    (n < (pagination_data.current_page + 3) && n <= 6 && (pagination_data.current_page <= 4)) || (n > (pagination_data.last_page - 1))
                                ) || (
                                    (n > (pagination_data.current_page - 3) && n > (pagination_data.last_page - 6) && (pagination_data.current_page > (pagination_data.last_page - 4))) ||
                                    (n === 1)
                                )
                            ) || (
                                (n > (pagination_data.current_page - 3)) && n < (pagination_data.current_page + 3)
                            )" class="page-numbers" v-on:click.prevent="goto(n)" v-html="n"></a>
                        <span v-else-if="(n === (pagination_data.current_page - 3)) || n === (pagination_data.current_page + 3)" class="page-numbers dots">…</span>
                    </template>
                </template>

                <a v-if="pagination_data.current_page < pagination_data.last_page" class="next page-numbers" v-on:click.prevent="goto(pagination_data.current_page + 1)"><i class="fa fa-caret-right"></i></a>
                <span v-else class="next page-numbers disabled" aria-disabled="true"><i class="fa fa-caret-right"></i></span>
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
                const t = this;

                if(typeof t.pagination_data.current_page === 'number' && t.currentPage !== t.pagination_data.current_page){
                    t.$emit('update:pagination_goto', t.pagination_data.current_page);
                    t.currentPage = t.pagination_data.current_page;
                } else {
                    t.$emit('update:pagination_goto', false);
                }
            }
        },
        methods: {
            goto(page){
                this.$emit('update:pagination_goto', page);
            }
        },
        data() {
            return {
                currentPage: 1
            };
        }
    }
</script>

