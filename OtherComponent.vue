<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col">
                <div v-if="typeof data.users !== 'undefined' && typeof data.users.data !== 'undefined' && Object.keys(data.users.data).length > 0" class="card-deck">
                    <div v-for="(user, index) in data.users.data" :key="index" class="card">
                        <h3 class="text-center p-1 m-0" v-html="user.id"></h3>
                    </div>
                </div>

                <h3 v-else-if="typeof data.users !== 'undefined' && typeof data.users.data !== 'undefined' && Object.keys(data.users.data).length === 0" class="text-center">No results found</h3>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'other-component',
        props: [
            'pagination_data'
        ],
        watch: {
            pagination_goto: {
                handler: 'getUsers',
                immediate: true
            }
        },
        methods: {
            getUsers(page = ''){
                const   t = this;

                if( page !== false &&
                    typeof page === 'number' &&
                    page !== t.data.users.current_page
                ){
                    page = '?page=' + page;

                    axiosUsers.get('/directory/' + routeName + page)
                        .then(response => {
                            t.data = response.data;
                            t.$emit('update:pagination_data', t.data.users);
                        });
                }
            }
        },
        mounted() {
            this.getUsers();
        },
        data() {
            return {
                data: {
                    users: {
                        current_page: 0
                    }
                }
            };
        }
    }
</script>
