<template>
    <div>
        <span>작성자<input class="name" type="text" v-model="user"></span>
        <span>댓글<input class="comment" type="text" v-model="comment"></span>
            <button @click="save">save</button>
            <ul>
                <li v-for="(msg, index) in messages" :key="index">
                    <p>{{ msg.user }}::{{ msg.comment }}</p>
                </li>
            </ul>
    </div>
</template>

        <script>
            export default {
                data() {
                    return {user: '', comment: '', messages: []}
                },
                methods: {
                    save() {
                        const message = {
                            user: this.user,
                            comment: this.comment
                        };

                        this
                            .messages
                            .unshift(message);
                        this.user = null;
                        this.comment = null;
                    }
                }
            }
</script>

<style scoped>
    .name {
        width: 10%;
        display: inline-block;
        margin-right: 1%;
    }
    .comment {
        width: 70%;
        display: inline-block;
        margin-right: 1%;
    }
</style>