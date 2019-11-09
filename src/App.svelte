<script>
    import lottie from 'lottie-web';

    let filename = '';
    const reader = new FileReader();

    reader.onload = ({ target: { result } }) => {
        try {
            document.getElementById('animation').innerHTML = "";
            lottie.loadAnimation({
                animationData: JSON.parse(result),
                autoplay: false,
                container: document.getElementById('animation'),
                renderer: 'svg',
            });
        } catch (e) {
            // We prevent the app from crashing but don't supply a message to the user,
            // and just log the error. This is not a mission critical application.
            console.log(e);
        }
    };

    const change = ({ target: { files } }) => {
        const file = files[0];
        reader.readAsText(file);
        filename = `${file.name.split('.')[0]}.svg`;
    };

    const reset = () => filename = "";

    const save = () => {
        const svg = document.getElementById('animation').children[0];
        const serializer = new XMLSerializer();
        const source = serializer.serializeToString(svg);

        // Create a hidden link to click that triggers the download
        const element = document.createElement('a');
        element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(source));
        element.setAttribute('download', filename);
        element.style.display = 'none';

        // Add the hidden link to the DOM
        document.body.appendChild(element);

        // Click the hidden link
        element.click();

        // Remove the hidden link from the DOM
        document.body.removeChild(element);
    }
</script>

<style>
    .wrapper {
        text-align: center;
        margin: 10vh auto 0 auto;
        max-width: 600px;
    }

    .btn {
        border: none;
        color: #0070f3;
        background-color: transparent;
        border-radius: 7px;
        cursor: pointer;
        display: inline-block;
        font-family: inherit;
        font-size: inherit;
        line-height: inherit;
        outline: none;
        padding: 0.25rem 0.5rem;
        text-decoration: none;
        transition: background 0.2s ease,color 0.2s ease,box-shadow 0.2s ease;
    }

    .btn:disabled {
        color: #888;
        background-color: #efefef;
        cursor: not-allowed;
        filter: grayscale(1);
        box-shadow: none;
    }

    .btn:hover {
        background: rgba(0,118,255,0.1);
    }

    .btn.cta {
        background-color: #0070f3;
        box-shadow: 0 4px 14px 0 rgba(0,118,255,0.39);
        color: white;
        height: 2.81rem;
        line-height: 2.8rem;
        margin: 0;
        padding: 0 3.5rem;
    }

    .btn.cta:hover {
        background: rgba(0,118,255,0.9);
        box-shadow: 0 6px 20px rgba(0,118,255,0.23);
    }

    p {
        color: #717171;
        font-weight: 400;
    }

    input[type="file"] {
        display: none;
    }

    #animation {
        margin: 2rem 0;
    }
</style>

<div class="wrapper">
    <h1>
        Lottie to SVG
    </h1>
    <p>Convert existing Lottie JSON data files to static SVGs</p>
    {#if filename === ''}
        <div>
            <label class="btn cta" for="input">Select source file</label>
            <input accept=".json" id="input" on:change="{change}" type="file">
        </div>
        {:else}
        <div>
            <button class="btn cta" disabled="{filename === ''}" on:click="{save}">Download SVG</button>
            <div id="animation"></div>
            <button class="btn" on:click="{reset}">Reset</button>
        </div>
    {/if}
</div>