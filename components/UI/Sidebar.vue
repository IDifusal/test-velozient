<template>
    <div class="sidebar text-white h-screen">
        <div class="h-20"></div>
        <div class="sidebar-item flex justify-center items-center p-2">
            <svg width="32" height="32" viewBox="0 0 24 24"><path fill="currentColor" d="M12 17a2 2 0 0 0 2-2a2 2 0 0 0-2-2a2 2 0 0 0-2 2a2 2 0 0 0 2 2m6-9a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V10a2 2 0 0 1 2-2h1V6a5 5 0 0 1 5-5a5 5 0 0 1 5 5v2h1m-6-5a3 3 0 0 0-3 3v2h6V6a3 3 0 0 0-3-3Z"/></svg>
         Passwords
        </div>
    </div>
</template>
<style scoped lang="scss">
.sidebar{
    @media(max-width:750px){
        visibility: hidden;
    }
    background: rgba(63, 74, 83, 1);
    &-item{
        background: #22313B;
        &:hover{
            cursor: pointer;
        }
    }
}
</style>