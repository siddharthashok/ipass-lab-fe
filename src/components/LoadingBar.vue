<template>
    <div :class="{ alternate: alt }" class="progress">
        <div class="indeterminate"></div>
    </div>
</template>

<script>
export default {
    name: 'LoadingBar',
    props: {
        alt: {
            type: Boolean,
            default: false
        }
    }
};
</script>

<style lang="scss" scoped>
/* Progress Bar */
$progress-bar-color: white !default;
$progress-bar-alt-color: #00a4ff !default;

// Progress Bar
.progress {
    position: fixed;
    top: 0;
    left: 0;
    height: 5px;
    display: block;
    width: 100%;
    background-color: rgba($progress-bar-color, 0.4);
    border-radius: 2px;
    background-clip: padding-box;
    margin: 0 0 1rem 0;
    overflow: hidden;
    z-index: 100000;

    .indeterminate {
        background-color: $progress-bar-color;
        &:before {
            content: '';
            position: absolute;
            background-color: inherit;
            top: 0;
            left: 0;
            bottom: 0;
            will-change: left, right;
            // Custom bezier
            animation: indeterminate 2.1s
                cubic-bezier(0.65, 0.815, 0.735, 0.395) infinite;
        }
        &:after {
            content: '';
            position: absolute;
            background-color: inherit;
            top: 0;
            left: 0;
            bottom: 0;
            will-change: left, right;
            // Custom bezier
            animation: indeterminate-short 2.1s
                cubic-bezier(0.165, 0.84, 0.44, 1) infinite;
            animation-delay: 1.15s;
        }
    }

    &.alternate {
        background-color: lighten($progress-bar-alt-color, 40%);
        .indeterminate {
            background-color: $progress-bar-alt-color;
        }
    }
}
@keyframes indeterminate {
    0% {
        left: -35%;
        right: 100%;
    }
    60% {
        left: 100%;
        right: -90%;
    }
    100% {
        left: 100%;
        right: -90%;
    }
}

@keyframes indeterminate-short {
    0% {
        left: -200%;
        right: 100%;
    }
    60% {
        left: 107%;
        right: -8%;
    }
    100% {
        left: 107%;
        right: -8%;
    }
}
</style>
