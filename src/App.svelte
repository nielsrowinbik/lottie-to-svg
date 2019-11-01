<div class="h-screen w-screen flex flex-col justify-center max-w-2xl m-auto">
    <h1 class="font-medium text-4xl text-center mb-2">
        Lottie to SVG
    </h1>
    <p class="text-center mb-16">Convert existing Lottie JSON data files to static SVGs</p>
    <div class="container mx-auto flex flex-row">
        <div class="container mx-auto flex flex-col items-center">
            <h2>Source</h2>
            <label for="file-upload" class="bg-grey-light hover:bg-grey text-grey-darkest font-bold py-2 px-4 rounded inline-flex items-center .cursor-pointer">
                Custom Upload
            </label>
            <input id="file-upload" type="file" class="hidden" />
            <p>or</p>
            <textarea class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded py-2 px-4 block w-full appearance-none leading-normal resize-none"></textarea>
        </div>
        <div class="container mx-auto flex flex-col items-center">
            <h2>Result</h2>
        </div>
    </div>
</div>