

<script lang="ts">
    import { authDataStore } from '$lib/stores';
    import { onMount } from "svelte";
    import { env } from "$env/dynamic/public";

    let file: any = null;
    let token: string = "";
    let returnedFileUrl: string | null = null;
    
    const handleFileInput = (event: any) => {
        file = event.target.files[0];
    };

    const handleFormSubmit = async (event: { preventDefault: () => void; }) => {
        event.preventDefault();

        const formData = new FormData();
        formData.append('file', file);

        const response = await fetch(`${env.PUBLIC_BACKEND_BASE_URL}/upload`, {
            method: 'POST',
            headers: {
                Authorization: `${token}`
            },
            body: formData
        });


        console.log(response);
        returnedFileUrl = await response.text()
    };

</script>

<div>
    <form on:submit={handleFormSubmit}>
        <label for="file-input">Choose a file:</label>
        <input type="file" id="file-input" on:change={handleFileInput} />
        
        <label for="permission code">Enter your upload permission code:</label>
        <input type="text" id="permission code" bind:value={token} />

        <button type="submit">Upload</button>
        {#if returnedFileUrl}
            <p>Returned download url:</p>
            <a href={env.PUBLIC_BACKEND_BASE_URL+returnedFileUrl}>{env.PUBLIC_BACKEND_BASE_URL}{returnedFileUrl}</a>
        {/if}
    </form>

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
        margin-top: 50px;
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