<template>
  <div>
    <div class="q-layout-padding">
      <div class="caption" style="margin-top: 120px;">
        This page has intended scroll so you can see multiple scenarios.
      </div>

      <div class="q-gutter-sm">
        <q-toggle v-model="toggle" class="z-max fixed-top" />
        <q-btn color="primary" label="Persistent">
          <q-menu
            v-model="toggle"
            ref="popover1"
            persistent
            transition-show="jump-down"
            @show="log('@show popover1 persistent')"
            @hide="log('@hide popover1 persistent')"
          >
            <q-list padding style="min-width: 100px">
              <q-item
                v-for="n in 20"
                :key="n"
                clickable
                v-close-menu
                @click="showNotify()"
                @keyup.native.13.32="showNotify()"
              >
                <q-item-section>Label</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </q-btn>

        <q-btn color="primary" icon="map">
          <q-menu @show="log('@show popover_map')" @hide="log('@hide popover_map')">
            <q-list style="min-width: 100px">
              <q-item
                v-for="n in 20"
                :key="n"
                clickable
                v-close-menu
                @click="showNotify()"
                @keyup.native.13.32="showNotify()"
              >
                <q-item-section>Label</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </q-btn>

        <q-btn color="primary" label="Cover">
          <q-menu cover @show="log('@show cover')" @hide="log('@hide cover')">
            <q-list style="min-width: 100px">
              <q-item
                v-for="n in 20"
                :key="n"
                clickable
                v-close-menu
                @click="showNotify()"
                @keyup.native.13.32="showNotify()"
              >
                <q-item-section>Label</q-item-section>
              </q-item>
            </q-list>
          </q-menu>
        </q-btn>

        <q-btn ref="target4" color="negative" label="Disabled Popover">
          <q-menu disable>
            This Popover content won't be shown because of "disable"
          </q-menu>
        </q-btn>
      </div>

      <div class="q-gutter-md q-my-md">
        <q-card class="q-mx-auto" style="width: 500px; max-width: 90vw;">
          <q-card-section class="bg-primary text-center">
            <q-btn push color="orange" label="Tap Me Large">
              <q-menu
                :fit="fit"
                :cover="cover"
                :anchor="anchor"
                :self="self"
                auto-close
              >
                <q-list style="min-width: 400px">
                  <q-item
                    v-for="n in 50"
                    :key="n"
                    clickable
                    @click="showNotify()"
                    @keyup.native.13.32="showNotify()"
                  >
                    <q-item-section>Label</q-item-section>
                  </q-item>
                </q-list>
              </q-menu>
            </q-btn>
            <q-btn push color="orange" label="Tap Me Small" class="on-right">
              <q-menu
                :fit="fit"
                :cover="cover"
                :anchor="anchor"
                :self="self"
              >
                <q-list>
                  <q-item
                    v-for="n in 5"
                    :key="n"
                    v-close-menu
                    clickable
                    @click="showNotify()"
                    @keyup.native.13.32="showNotify()"
                  >
                    <q-item-section>Label</q-item-section>
                  </q-item>
                </q-list>
              </q-menu>
            </q-btn>
          </q-card-section>

          <div class="text-weight-bold text-center q-my-md">
            Configure the Popover for button above.
          </div>
          <div class="text-center" v-if="cover">
            <q-chip square color="primary" text-color="white">
              cover
            </q-chip>
            <q-chip square color="primary" text-color="white">
              anchor="{{ anchor }}"
            </q-chip>
          </div>
          <div class="text-center" v-else>
            <q-chip v-if="fit" square color="primary" text-color="white">
              fit
            </q-chip>
            <q-chip square color="primary" text-color="white">
              anchor="{{ anchor }}"
            </q-chip>
            <q-chip square color="primary" text-color="white">
              self="{{ self }}"
            </q-chip>
          </div>
          <div class="row flex-center q-my-sm q-gutter-md">
            <q-toggle v-model="fit" label="Fit" />
            <q-toggle v-model="cover" label="Cover" />
          </div>
          <q-card-section class="row" :class="cover ? 'justify-center' : ''">
            <div class="column items-center col-6">
              <div class="text-weight-bold">
                Anchor Origin
              </div>
              <div class="flex q-gutter-sm">
                <div class="column">
                  <div>Vertical</div>
                  <q-radio v-model="anchorOrigin.vertical" val="top" label="Top" />
                  <q-radio v-model="anchorOrigin.vertical" val="center" label="Center" />
                  <q-radio v-model="anchorOrigin.vertical" val="bottom" label="Bottom" />
                </div>
                <div class="column">
                  <div>Horizontal</div>
                  <q-radio v-model="anchorOrigin.horizontal" val="left" label="Left" />
                  <q-radio v-model="anchorOrigin.horizontal" val="middle" label="Middle" />
                  <q-radio v-model="anchorOrigin.horizontal" val="right" label="Right" />
                </div>
              </div>
            </div>

            <div class="column items-center col-6" v-if="!cover">
              <div class="text-weight-bold">
                Self Origin
              </div>
              <div class="flex q-gutter-sm">
                <div class="column">
                  <div>Vertical</div>
                  <q-radio v-model="selfOrigin.vertical" val="top" label="Top" />
                  <q-radio v-model="selfOrigin.vertical" val="center" label="Center" />
                  <q-radio v-model="selfOrigin.vertical" val="bottom" label="Bottom" />
                </div>
                <div class="column">
                  <div>Horizontal</div>
                  <q-radio v-model="selfOrigin.horizontal" val="left" label="Left" />
                  <q-radio v-model="selfOrigin.horizontal" val="middle" label="Middle" />
                  <q-radio v-model="selfOrigin.horizontal" val="right" label="Right" />
                </div>
              </div>
            </div>
          </q-card-section>
        </q-card>

        <q-card class="q-mx-auto" style="width: 500px; max-width: 90vw;">
          <q-card-section>
            <div class="q-gutter-sm">
              <q-toggle label="touch-position" v-model="touchPosition" />
              <q-toggle label="context-menu" v-model="contextMenu" />
            </div>
          </q-card-section>
          <q-img src="https://cdn.quasar-framework.org/img/material.png" style="height: 100px">
            <q-menu :touch-position="touchPosition" :context-menu="contextMenu">
              <q-list>
                <q-item
                  v-for="n in 5"
                  :key="n"
                  v-close-menu
                  clickable
                  @click="showNotify()"
                  @keyup.native.13.32="showNotify()"
                >
                  <q-item-section>Label</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-img>
        </q-card>

        <q-card class="q-mx-auto" style="width: 500px; max-width: 90vw;">
          <q-card-section>
            <q-toggle v-model="vIfTest" label="v-if test" />
          </q-card-section>
          <q-img src="https://cdn.quasar-framework.org/img/material.png" style="height: 100px" v-if="vIfTest">
            <div class="absolute-bottom-right">
              attached to q-img
            </div>
            <q-menu touch-position>
              <q-list>
                <q-item
                  v-for="n in 5"
                  :key="n"
                  v-close-menu
                  clickable
                  @click="showNotify()"
                  @keyup.native.13.32="showNotify()"
                >
                  <q-item-section>Label</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-img>
          <q-img src="https://cdn.quasar-framework.org/img/parallax2.jpg" style="height: 100px">
            <div class="absolute-bottom-right">
              attached to q-menu
            </div>
            <q-menu touch-position v-if="vIfTest">
              <q-list>
                <q-item
                  v-for="n in 5"
                  :key="n"
                  v-close-menu
                  clickable
                  @click="showNotify()"
                  @keyup.native.13.32="showNotify()"
                >
                  <q-item-section>Label</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-img>
        </q-card>

        <q-card class="q-mx-auto" style="width: 500px; max-width: 90vw;">
          <q-card-section>
            <div class="row items-center q-gutter-sm">
              <q-chip square color="primary" text-color="white">
                target
              </q-chip>
              <q-radio v-model="targetEl" :val="false" label="false (no target whatsoever)" />
              <q-radio v-model="targetEl" :val="true" label="true (original parent)" />
              <q-radio v-model="targetEl" val="#target-img-1" label="#target-img-1" />
              <q-radio v-model="targetEl" val="#target-img-2" label="#target-img-2" />
              <q-radio v-model="targetEl" val="#bogus" label="#bogus" />
            </div>
          </q-card-section>
          <q-img src="https://cdn.quasar-framework.org/img/material.png" id="target-img-1" style="height: 100px">
            <div class="absolute-bottom-right">
              #target-img-1
            </div>
          </q-img>
          <q-img src="https://cdn.quasar-framework.org/img/parallax2.jpg" id="target-img-2" style="height: 100px">
            <div class="absolute-bottom-right">
              #target-img-2
            </div>
          </q-img>
          <q-img src="https://cdn.quasar-framework.org/img/blueish.jpg" style="height: 100px">
            <div class="absolute-bottom-right">
              Original parent
            </div>
            <q-menu touch-position :target="targetEl">
              <q-list>
                <q-item
                  v-for="n in 5"
                  :key="n"
                  v-close-menu
                  clickable
                  @click="showNotify()"
                  @keyup.native.13.32="showNotify()"
                >
                  <q-item-section>Label</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-img>
        </q-card>

        <q-card class="q-mx-auto" style="width: 500px; max-width: 90vw;">
          <q-card-section>
            Menu in menu
          </q-card-section>
          <q-img src="https://cdn.quasar-framework.org/img/parallax1.jpg" style="height: 100px">
            <q-menu touch-position>
              <q-list>
                <q-item
                  v-close-menu
                  clickable
                >
                  <q-item-section>v-close-menu</q-item-section>
                </q-item>

                <q-item
                  v-for="n in 3"
                  :key="n"
                  clickable
                >
                  <q-item-section>Label</q-item-section>
                  <q-item-section side>
                    <q-icon name="keyboard_arrow_right" />
                  </q-item-section>

                  <q-menu anchor="top right" self="top left">
                    <q-list>
                      <q-item
                        v-close-menu
                        clickable
                      >
                        <q-item-section>v-close-menu</q-item-section>
                      </q-item>

                      <q-item
                        v-for="x in 3"
                        :key="x"
                        clickable
                      >
                        <q-item-section>Submenu Label</q-item-section>
                        <q-item-section side>
                          <q-icon name="keyboard_arrow_right" />
                        </q-item-section>
                        <q-menu auto-close anchor="top right" self="top left">
                          <q-list>
                            <q-item
                              v-for="y in 3"
                              :key="y"
                              clickable
                            >
                              <q-item-section>3rd level Label</q-item-section>
                            </q-item>
                          </q-list>
                        </q-menu>
                      </q-item>
                    </q-list>
                  </q-menu>
                </q-item>
              </q-list>
            </q-menu>
          </q-img>
        </q-card>
      </div>

      <div style="margin-bottom: 700px;" />

      <q-btn color="secondary" class="fixed-top-right" icon="directions" style="top: 65px; right: 16px;">
        <q-menu ref="popover3">
          <q-img
            src="https://cdn.quasar-framework.org/img/map.png"
            style="height: 150px; width: 200px;"
            @click.native="showNotify(), $refs.popover3.hide()"
            @keyup.13.32.native="showNotify(), $refs.popover3.hide()"
            tabindex="0"
          />
        </q-menu>
      </q-btn>

      <q-btn color="accent" class="fixed-bottom-right" icon="plus_one" style="bottom: 10px; right: 16px;">
        <q-menu ref="popover4">
          <div class="group" style="width: 220px; text-align: center;">
            <q-btn icon="thumb_up" flat color="primary" @click="showNotify(), $refs.popover4.hide()" />
            <q-btn icon="thumb_down" flat color="primary" @click="showNotify(), $refs.popover4.hide()" />
            <q-btn icon="share" flat color="secondary" @click="showNotify(), $refs.popover4.hide()" />
          </div>
        </q-menu>
      </q-btn>
    </div>

    <q-btn icon="menu" color="primary" class="fixed-bottom-left" style="bottom: 10px; left: 10px;">
      <q-menu ref="popover5">
        <q-list style="min-width: 200px">
          <q-item
            v-for="n in 20"
            :key="n"
            clickable
            @click.native="showNotify(), $refs.popover5.hide()"
            @keyup.native.13.32="showNotify(), $refs.popover5.hide()"
          >
            <q-item-section>Label</q-item-section>
          </q-item>
        </q-list>
      </q-menu>
    </q-btn>
  </div>
</template>

<script>
export default {
  data () {
    let list = []
    for (let i = 0; i < 26 * 30; i += 1) {
      const c = String.fromCharCode(97 + (i % 26))
      const v = `${c}${c}${c}${c}${c}#${i}`
      list.push({ label: v, value: v })
    }
    return {
      fit: false,
      cover: false,
      toggle: false,
      anchorOrigin: { vertical: 'bottom', horizontal: 'left' },
      selfOrigin: { vertical: 'top', horizontal: 'left' },
      terms: '',
      modelDate: null,
      model: 30,
      min: 0,
      max: 50,
      list,

      vIfTest: true,
      touchPosition: true,
      contextMenu: true,
      targetEl: '#target-img-1'
    }
  },
  computed: {
    anchor () {
      return `${this.anchorOrigin.vertical} ${this.anchorOrigin.horizontal}`
    },
    self () {
      return `${this.selfOrigin.vertical} ${this.selfOrigin.horizontal}`
    }
  },
  methods: {
    showNotify () {
      this.$q.notify((this.$q.platform.is.desktop ? 'Clicked' : 'Tapped') + ' on a QMenu item')
    },
    log (msg) {
      console.log(msg)
    }
  }
}
</script>
