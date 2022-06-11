<template>
    <div class="wallet">
            <header class="wallet__header">
                <div class="wallet__headerleft">
                    <figure>
                        <img src='@/assets/images/pink-circle.png'/>
                    </figure>
                </div>
                <div class="wallet__headerright">
                    <div class="wallet__headersec" @click="openslide('transactions')">
                        <div class="wallet__headersec--dropdown">
                            <span>Transactions</span>
                        </div>
                    </div>
                    <div class="wallet__headersec" @click="openslide('cards')">
                        <div class="wallet__headersec--dropdown">
                            <span>Cards</span>
                        </div>
                    </div>
                    <div class="wallet__headersec" @click="openslide('notifications')">
                        <div class="wallet__headersec--dropdown">
                            <span class="notification">10</span>
                            <span class="svg">
                                <svg>
                                    <use xlink:href="@/assets/imgs/sprite.svg#icon-bell" />
                                </svg>
                            </span>
                        </div>
                    </div>
                </div>
            </header>

            <div class="wallet__body">
                <div class="wallet__sidenav">
                    <div class="wallet__sidenav--item" :class="{
                        'current': currentroute === 'overview'
                    }">
                        <router-link to="/overview">
                            <span>
                                <svg>
                                    <use xlink:href="@/assets/imgs/sprite.svg#icon-bar-chart" />
                                </svg>
                            </span>
                            <span>Overview</span>
                        </router-link>
                    </div>
                    <div class="wallet__sidenav--item" :class="{
                        'current': currentroute === 'transfer'
                    }">
                    </div>
                    <div class="wallet__sidenav--item">
                        <router-link to="/profile">
                            <span>
                                <svg>
                                    <use xlink:href="@/assets/imgs/sprite.svg#icon-profile" />
                                </svg>
                            </span>
                            <span>Profile</span>
                        </router-link>
                    </div>
                    <div class="wallet__sidenav--item">
                        <router-link to="/password">
                            <span>
                                <svg>
                                    <use xlink:href="@/assets/imgs/sprite.svg#icon-profile" />
                                </svg>
                            </span>
                            <span>Password</span>
                        </router-link>
                    </div>
                    <div class="wallet__sidenav--item logout" @click="logout">
                        <div>
                            <span>
                                <svg>
                                    <use xlink:href="@/assets/imgs/sprite.svg#icon-info" />
                                </svg>
                            </span>
                            <span>Logout</span>
                        </div>
                    </div>
                </div>  

                <div class="wallet__container">
                    <div class="wallet__top">
                        <div class="wallet__top--left">
                            <h1 class="wallet__top--h1">{{title}}</h1>
                        </div>
                        <div class="wallet__top--right">
                            <!--<div class="wallet__top--rightbtns">
                                <span class="wallet__top--rightbtn">
                                    <button @click="btnselect('transfer')" :class="{ current: current === 'transfer' }">Transfer</button>
                                </span>
                                <span class="wallet__top--rightbtn">
                                    <button @click="btnselect('withdraw')" :class="{ current: current === 'withdraw' }">Withdraw</button>
                                </span>
                            </div>-->
                        </div>
                    </div>
                    <div class="wallet__base">
                        <slot name="base"></slot>
                    </div>
                </div>              
            </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                current: 'overview'
            }
        },
        props: ['title', 'openslide'],
        methods: {
            btnselect(val) {
                this.current = val;
            },
            logout() {
                localStorage.removeItem('norduserxtxtxt');
                localStorage.removeItem('nordtokenxtxtxt');
                this.$router.push('/');
            }
        },
        computed: {
            currentroute() {
                return this.$route.name;
            }
        }
    }
</script>

<style lang="scss" scoped>
  @function scaleValue($value) {
    @return calc(
      #{$value} * (clamp(350px, 100vw, 3840px) / var(--ideal-viewport-width))
    );
  }

    .wallet {
        color: #fff;

        &__header {
            padding: #{scaleValue(20)} #{scaleValue(90)};
            border-bottom: 1px solid rgba(255, 255, 255, .2);
            color: rgb(254, 176, 25);
            font-size: #{scaleValue(25)};
            display: flex;
            align-items: center;
            justify-content: space-between;

            @media only screen and (max-width: 414px) { 
                font-size: #{scaleValue(90)};
                padding: #{scaleValue(70)} #{scaleValue(90)};
            }
        }

        &__headerleft {
            position: relative;
            display: flex;
            align-items: center;
            cursor: pointer;

            & figure {
                position: absolute;
                top: 0;
                left: 0;
                height: #{scaleValue(40)};
                width: #{scaleValue(40)};
                display: flex;
                justify-content: center;
                align-items: center;
                transform: translateY(#{scaleValue(-20)});

                & img {
                    object-fit: cover;
                    height: 100%;
                    width: 100%;
                }
            }

            & p {
                margin-left: #{scaleValue(40)};
            }
        }

        &__headerright {
            color: #fff;
            font-size: #{scaleValue(18)};
            font-weight: 400;
            display: flex;
            align-items: center;
        }

        &__headersec {
            position: relative;
            margin-left: #{scaleValue(55)};
            cursor: pointer;

            &--dropdown {
                color: #fff;

                &:hover {

                    & ~ .wallet__headersec--dropdowns {
                        display: flex;
                    }
                }

                & figure {
                    height: #{scaleValue(20)};
                    width: #{scaleValue(20)};
                    transform: translateY(#{scaleValue(-3)});

                    & img {
                        display: inline-block;
                        border-radius: 50%;
                        object-fit: cover;
                        height: 100%;
                        width: 100%;
                    }
                }

                & span {

                    &.svg {

                        & svg {
                            fill: #fff;
                            height: #{scaleValue(20)};
                            width: #{scaleValue(20)};
                        }
                    }

                    &.notification {
                        background: red;
                        border-radius: 3rem;
                        position: absolute;
                        top: #{scaleValue(-11)};
                        right: #{scaleValue(-9)};
                        height: #{scaleValue(20)};
                        width: #{scaleValue(20)};
                        font-size: #{scaleValue(10)};
                        display: flex;
                        justify-content: center;
                        align-items: center;
                    }
                }               
            }

            &--dropdowns {
                position: absolute;
                top: #{scaleValue(16)};
                right: 0;
                background: rgb(30, 35, 41);
                color: #fff;
                width: #{scaleValue(180)}; 
                display: none;
                flex-direction: column;
                -webkit-box-shadow: 0 0 7px 0 rgba(0, 0, 0, .09);
                -moz-box-shadow: 0 0 7px 0 rgba(0, 0, 0, .09);
                -ms-box-shadow: 0 0 7px 0 rgba(0, 0, 0, .09);
                box-shadow: 0 0 7px 0 rgba(0, 0, 0, .09);
                border-radius: 2px;

                &:hover {
                    display: flex;
                }

                & span {
                    display: inline-block;
                    padding: #{scaleValue(20)} #{scaleValue(15)};

                    &:hover {
                        background: #000000;
                    }
                }
            }
        }

        &__body {
            display: flex;
        }

        &__sidenav {
            height: 100vh;
            position: absolute;
            width: #{scaleValue(180)};
            top: #{scaleValue(62)};
            left: 0;
            color: #fff;
            border-right: 1px solid rgba(255, 255, 255, .2);
            padding-top: #{scaleValue(50)};

            &--item {
                margin-bottom: #{scaleValue(30)};
                cursor: pointer;
                font-size: #{scaleValue(18)};

                &.logout {
                    position: absolute;
                    bottom: #{scaleValue(100)};
                    width: #{scaleValue(180)};
                    right: 0;
                }

                a, &.logout {
                    display: block;
                    text-decoration: none;
                    outline: none;
                    cursor: pointer;
                    color: #fff;
                    padding: #{scaleValue(20)} #{scaleValue(30)};
                }

                & span {
                    display: inline-block;

                    &:nth-child(1) {
                        margin-right: #{scaleValue(10)};

                        & svg {
                            fill: #fff;
                            height: #{scaleValue(15)};
                            width: #{scaleValue(15)};
                        }
                    }
                }

                &:hover {
                    background: rgb(30, 35, 41)
                }

                &.current {
                    background: rgb(30, 35, 41)
                }
            }
        }

        &__container {
            display: flex;
            flex-direction: column;
            width: #{scaleValue(1350)};
        }

        &__top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #000;
            padding: #{scaleValue(30)} #{scaleValue(30)};

            &--h1 {
                font-size: #{scaleValue(30)};
                font-weight: 700;
                text-transform: capitalize;
                margin-left: #{scaleValue(220)};
            }

            &--rightbtn {

                & button {
                    border: none;
                    background: rgb(71, 77, 87);
                    padding: #{scaleValue(13)} #{scaleValue(20)};
                    color: #fff;
                    font-weight: 500;
                    border-radius: 2px;
                    font-size: #{scaleValue(13)};
                    margin-left: #{scaleValue(25)};
                    cursor: pointer;

                    &.current {
                        background: #474DFF;
                        color: #fff;

                        &:hover {
                            background: rgba(#474DFF, .8);
                        }
                    }

                    &:hover {
                        background: rgba(71, 77, 87, .8);
                    }
                }
            }
        }

        &__base {
            //padding: #{scaleValue(30)} #{scaleValue(30)};
            display: flex;
            justify-content: space-between;
            padding-left: #{scaleValue(250)};
        }
    }
</style>