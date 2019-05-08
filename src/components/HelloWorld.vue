<template>
    <div class="hello">
        <div class="form">
            <div class="control">
                <button class="add" type="button" @click="addQuest">
                    Ajouter
                </button>
            </div>
            <div class="control">
                <button type="button" @click="exportData">
                    Exporter
                </button>
            </div>
            <div class="control">
                <label for="importFile">Impoter</label>
                <input type="file" id="importFile" ref="importFile" @change="importData">
            </div>
        </div>
        <ul class="quests" v-for="questItem in quests">

            <li class="quest-item">
                <div class="status">
                    <input type="checkbox"  v-model="questItem.checked" :checked="questItem.checked">
                </div>
                <div class="title">
                    <textarea v-model="questItem.title" placeholder="Title"></textarea>
                </div>
                <svg preserveAspectRatio="none" viewBox="0 0 40 40" height="40px" width="40px">
                    <polygon points="0,0 30,0 0,40" />
                </svg>
            </li>
        </ul>
    </div>
</template>

<script>

    import Quest from './Quest'

    export default {
        components: {
           Quest
        },
        name: 'HelloWorld',
        data() {
            return {
                quests: [
                    {
                        
                        title: 'Quete1',
                        checked: true,
                    },
                    {
                        title: 'Quete2',
                        checked: false,
                    }
                ]
            }
        },
        methods: {
            addQuest() {
                this.quests.push({
                    title: '',
                    checked: false
                })
            },
            exportData() {
                const   filename = 'test.json',
                        data = this.quests,
                        type = 'text/plain';

                const   a = document.createElement("a");
                a.style.display = 'none';
                document.body.appendChild(a);

                console.log(JSON.stringify(data));

                a.href = window.URL.createObjectURL(
                    new Blob([JSON.stringify(data)], { type })
                );

                a.setAttribute('download',filename);

                a.click();

                window.URL.revokeObjectURL(a.href);
                document.body.removeChild(a);

            },
            importData() {

                const fileInput = this.$refs['importFile'];
                let files = fileInput.files;
                let file = files[0];
                let reader = new FileReader();
                let that = this;
                reader.onload = function(event) {
                    let data = JSON.parse(event.target.result);
                    console.log(data);
                    console.log(that.quests);
                    for(let i = 0; i < data.length; i++) {
                        let item = data[i];
                        that.quests.push(item);
                    }
                }
                reader.readAsText(file)

            }
        }
    }
</script>

<style scoped>

    .form {
        padding: 5px;
        margin-bottom: 30px;
        font-size: 12px;
        text-transform: uppercase;
        display: flex;
        justify-content: space-between;
    }

    .form .control {

    }

    .form button {
        appearance: none;
        background: #eee;
        color: #333;
        border: 0;
        display: inline-block;
        padding: 7px 15px;
        font-size: 12px;
        text-transform: uppercase;
    }

    button.add {
        background: greenyellow;
    }

    .quest-item {
        padding: 0.5rem;
        margin: 0.5rem 60px 0.5rem 0.5rem;
        color: #fff;
        background: #333;
        display: flex;
        position: relative;
    }
    .quest-item svg {
        display: block;
        position: absolute;
        right: -40px;
        top: 0;
        height: 100%;
        bottom: 0;
        width: 40px;
        fill: #333;
    }

    .status {
        display: inline-block;
    }
    .title {
        display: inline-block;
        flex-basis: 100%;
    }
    input[type='checkbox'] {
        display: block;
        width: 30px;
        height: 30px;
        background: #333;
    }
    textarea {
        border: 0;
        background: transparent;
        display: block;
        width: 100%;
        font-size: 24px;
        line-height: 1;
        color: #fff;
        min-height: 40px;
    }
</style>
