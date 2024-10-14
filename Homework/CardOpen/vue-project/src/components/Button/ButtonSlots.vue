<template>
    <div><h3>
        <slot></slot>
        Button component</h3>
    <br>
    <button>
        <slot>
            Default Value
        </slot>
    </button>
    </div>
</template>