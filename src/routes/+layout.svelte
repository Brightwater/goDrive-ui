<script lang="ts">
    import Navigation2 from '$lib/components/Navigation2.svelte';
</script>

<div>
    <Navigation2/>
    <main>
        <slot/>
    </main>
</div>

<style lang="scss">
    $textColor: rgba(175, 175, 215, 1);
    $rowColorA: rgba(35, 35, 85, 1);
    $outlinecolor: rgb(35, 35, 76, 1);
    $rowColorB: rgba(55, 55, 85, 1);
    $theadColor: rgba(50, 50, 90, 1);

    div {
        color: $textColor;
        height: 100%;
    }
    
    form {
        
        max-width: 500px;
        margin: 0 auto;
        margin-top: 100px;
        display: flex;
        flex-direction: column;

        label {
            margin: 10px 0;
        }

        input {
            padding: 10px;
            border-radius: 5px;
            border: 1px solid $outlinecolor;
            color: $textColor;
            background-color: $rowColorA;
            margin-bottom: 20px;
            width: 100%;
            box-sizing: border-box;

            &:focus {
                outline: none;
                border-color: #007bff;
            }
        }

        button {
            background-color: $theadColor;
            color: $textColor;
            border: none;
            border-radius: 5px;
            padding: 10px 20px;
            cursor: pointer;

            &:hover {
                background-color: $rowColorA;
            }

            &:focus {
                outline: none;
            }
        }
    }

    main {
        height: 93.75vh;
        overflow: auto;
    }
    ::-webkit-scrollbar {
        width: 10px;
        height: 10px;
        padding-top: 50px;
    }
    ::-webkit-scrollbar-thumb {
        background-color: $theadColor;
    }
    ::-webkit-scrollbar-corner {
        background-color: $rowColorA;
    }
    
</style>