<template>
    <section class="bg-block">
        <div class="container">
            <VeeForm class="table-box" @submit="onSubmit" v-slot="{ errors}">
                <h2 class="title">{{ store.language_txt.order?.text_information }}</h2>
                <div class="my-4">
                    <nuxt-link :to="prev_page" class="btn link">{{ store.language_txt.default?.text_back }}</nuxt-link>
                </div>
                <div class="row" v-if="userinfo">
                    <div class="col-lg-6 px-4 mb-lg-0 mb-4">
                        <h3 class="title fs-3 mb-4">{{store.language_txt.order.text_salesperson_information}}</h3>
                        <div class="row bg-body p-4" style="border-radius: 5px;">
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                    <span class="col-4 ">{{store.language_txt.order.column_dealer_code}}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.employer_company_code }}</div>
                                    <div class="col" v-else>{{ order_info.dealer_code }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{ store.language_txt.order.column_tax_id_num }}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.tax_id_num }}</div>
                                    <div class="col" v-else>{{ order_info.dealer?.tax_id_number }}</div>
                                </div>
                            </div>
                            <div class="col-md-12  mb-2">
                                <div class="user-data">
                                    <span class="col-xxl-2 col-4">{{ store.language_txt.order.column_company_name }}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.employer_company_name }}</div>
                                    <div class="col" v-else>{{ order_info.dealer_name }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                    <span class="col-4">{{ store.language_txt.order.column_salesperson_name }}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.name }}</div>
                                    <div class="col" v-else>{{ order_info.salesperson_name }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.order.column_salesperson_email}}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.email }}</div>
                                    <div class="col" v-else>{{ order_info.salesperson_email }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.order.column_salesperson_mobile}}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.mobile }}</div>
                                    <div class="col" v-else>{{ order_info.salesperson_mobile }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.order.column_salesperson_telephone}}</span>
                                    <div class="col" v-if="!order_id">{{ userinfo.telephone }}</div>
                                    <div class="col" v-else>{{ order_info.salesperson_telephone }}</div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{ store.language_txt.member.column_country }}</span>
                                    <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.country_name }}</div>
                                        <div v-else>{{ order_info.shipping_country_code }}</div>
                                    </div>
                                    <div class="col" v-else></div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.member.column_zip_code}}</span>
                                    <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.zip_code }}</div>
                                        <div v-else>{{ order_info.shipping_zip_code }}</div>
                                    </div>
                                    <div class="col" v-else></div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.member.column_state}}</span>
                                    <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.state }}</div>
                                        <div v-else>{{ order_info.shipping_state }}</div>
                                    </div>
                                    <div class="col" v-else></div>
                                </div>
                            </div>
                            <div class="col-xxl-6 col-12  mb-2">
                                <div class="user-data">
                                     <span class="col-4 ">{{store.language_txt.member.column_city}}</span>
                                     <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.city }}</div>
                                        <div v-else>{{ order_info.shipping_city }}</div>
                                     </div>
                                     <div class="col" v-else></div>
                                </div>
                            </div>
                            <div class="col-md-12  mb-2">
                                <div class="user-data">
                                    <span class="col-2">{{ store.language_txt.member.column_address1 }}</span>
                                    <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.address1 }}</div>
                                        <div v-else>{{ order_info.shipping_address1 }}</div>
                                    </div>
                                    <div class="col" v-else></div>
                                </div>
                            </div>
                            <div class="col-md-12  mb-2">
                                <div class="user-data">
                                    <span class="col-2">{{ store.language_txt.member.column_address2 }}</span>
                                    <div class="col" v-if="is_ship_to_me">
                                        <div v-if="!order_id">{{ userinfo.address2 }}</div>
                                        <div v-else>{{ order_info.shipping_address2 }}</div>
                                    </div>
                                    <div class="col" v-else></div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-6 px-4 d-flex flex-column">
                        <h3 class="title fs-3 mb-4">{{store.language_txt.order.text_customer_information}}</h3>
                        <div class="box_shadow flex-auto p-4 px-5" style="border-radius: 5px;">
                            <div class="col-md-12 mb-3">
                                <label class="col-3 form-label"> <span class="text-danger">*</span>{{store.language_txt.order.column_shipping_to}}</label>
                                <VeeField 
                                    as="select" 
                                    name="delivery_method" 
                                    :class="{ 'error': errors['delivery_method']}"
                                    class="form-select"
                                    v-model="order_info.delivery_method"
                                    rules="required"
                                    >
                                    <option value="pickup">{{ store.language_txt.order.text_delivery_method_pickup }}</option>
                                    <option value="delivery">{{ store.language_txt.order.text_delivery_method_delivery }}</option>
                                </VeeField>
                                <VeeErrorMessage class="error__label" name="delivery_method" />
                            </div>
                            <div class="col-md-12 mb-3">
                                <label class="col-3 form-label"> <span class="text-danger">*</span>{{store.language_txt.order.column_customer_first_name}}</label>
                                <VeeField 
                                    type="text" 
                                    class="form-control" 
                                    :class="{ 'error': errors['customer_first_name'] }" 
                                    name="customer_first_name"
                                    v-model="order_info.customer_first_name"
                                    rules="required"/>
                                <VeeErrorMessage class="error__label" name="customer_first_name" />
                            </div>
                            <div class="col-md-12 mb-3">
                                <label class="col-3 form-label"> <span class="text-danger">*</span>{{store.language_txt.order.column_customer_last_name}}</label>
                                <VeeField 
                                    type="text" 
                                    class="form-control" 
                                    :class="{ 'error': errors['customer_last_name'] }" 
                                    name="customer_last_name" 
                                    v-model="order_info.customer_last_name"
                                    rules="required"/>
                                <VeeErrorMessage class="error__label" name="customer_last_name" />
                            </div>
                            <div class="col-md-12 mb-3">
                                <label class="col-3 form-label"> <span class="text-danger">*</span>{{ store.language_txt.order.column_side_mark }}</label>
                                <VeeField 
                                    type="text" 
                                    class="form-control" 
                                    :class="{ 'error': errors['side_mark'] }"
                                    name="side_mark" 
                                    v-model="order_info.side_mark"
                                    rules="required"/>
                                <VeeErrorMessage class="error__label" name="side_mark" />
                            </div>
                            <div class="col-md-12 mb-3">
                                <label class="col-3 form-label">{{store.language_txt.order.text_option_section_note}}</label>
                                <VeeField 
                                    as="textarea"
                                    class="form-control" 
                                    :class="{ 'error': errors['note'] }"
                                    v-model="order_info.note"
                                    name="note"/>
                                <VeeErrorMessage class="error__label" name="note" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="text-center mt-5">
                    <button type="submit" class="btn sent_go" v-if="order_id && is_Draft">{{store.language_txt.default?.text_save}}</button>
                    <button type="submit" class="btn sent_go" v-if="!order_id">{{store.language_txt.default.text_continue}}</button>
                </div>
            </VeeForm>
        </div>
    </section>




</template>


<script setup>
const store = useStore()
const router = useRouter()
const route = useRoute()
const order_id = route.query.id

const userinfo = ref()

const order_info = ref({})

const text = ref()


const is_ship_to_me = computed(()=>{
    return order_info.value.delivery_method == 'delivery'
})

const is_Draft = computed(() =>{
    return order_info.value.status_code == 'Draft'
})



// 返回的路徑
const prev_page = computed(()=>{
    return order_id? `/order-list/item?id=${order_id}`:'/home'
})



const onSubmit = async(values)=>{
    store.show_loading(true)
    const url = `${store.baseUrl}api/v2/sales/orders/header/save?locale=${store.language}`
    const data = {
        // 運送方式
        delivery_method:values.delivery_method,
        // 經銷商(資訊)
        dealer_id:userinfo.value.employer_company_id,
        dealer_name:userinfo.value.employer_company_name,
        employer_company_code:userinfo.value.employer_company_code,
        // 業務
        salesperson_id:userinfo.value.id,
        salesperson_first_name:userinfo.value.first_name,
        salesperson_last_name:userinfo.value.last_name,
        salesperson_email:userinfo.value.email,
        salesperson_telephone:userinfo.value.telephone || "",
        salesperson_mobile:userinfo.value.mobile || "",
        
        // 客戶
        customer_first_name:values.customer_first_name,
        customer_last_name:values.customer_last_name,
        shipping_recipient:values.customer_last_name + values.customer_first_name,
        customer_email:userinfo.value.email,
        status_code:"Draft",
        side_mark:values.side_mark,
        note:values.note || "",
        tax:userinfo.value.tax_id_number || "",
    }
    if(is_ship_to_me.value && (order_info.value.salesperson_id == userinfo.value.user_id || !order_id)){
        // 運送
        data.shipping_country_code = userinfo.value.country_code || ""
        // data.shipping_country_name = userinfo.value.country_name || "",
        data.shipping_zip_code = userinfo.value.zip_code || ""
        data.shipping_state = userinfo.value.state || ""
        data.shipping_city = userinfo.value.city || ""
        data.shipping_address1 = userinfo.value.address1 || ""
        data.shipping_address2 = userinfo.value.address2 || ""
    }
    if(order_id){
        data.order_id = order_id
        data.material = order_info.value.material
        data.quantity = order_info.value.quantity
        data.sqm = order_info.value.sqm
        data.status_code = data.status_code
    }
    // console.log(data);
    try{
        const res = await fetch(url,{
            method:"POST",
            headers:{
                "Content-Type": "application/json",
                "Authorization": "Bearer " + store.userData.jwtToken,
                "X-CLIENT-IPV4":store.userData.loginIpAddress
            },
            body:JSON.stringify(data)
        })
        const res_data = await res.json()
        // console.log(res);
        // console.log(res_data);
        if(res.ok && order_id ){
            // 路由參數有id則返回列表頁
            router.push(`/order-list/item?id=${order_id}`)
        }else if(res.ok && res_data.order_id){
            // 則往新增頁
            router.push(`create_order/order?id=${res_data.order_id}`)
        }
    }catch(err){
        console.log(err);
    }
    store.show_loading(false)
}

// 會員資料
const get_data = async()=>{
    const data = await store.get_user_data()
    userinfo.value = data
    // console.log('會員',userinfo.value);
}

// 訂單資料
const get_order_data = async()=>{
    const url = `${store.baseUrl}api/v2/sales/orders/info?locale=${store.language}&equal_id=${order_id}`
    try{
        const res = await fetch(url,{
            headers:{
                "Authorization": "Bearer " + store.userData.jwtToken
            },
        })
        const res_data = await res.json()
        if(res.ok && res_data.success){
          order_info.value = res_data.response
          console.log(order_info.value);
            // 不是草稿且有訂單id則不能修改
            if (!is_Draft.value && order_id) {
                nextTick(() => {
                    $('.table-box input').attr('disabled', true)
                    $('.table-box select').attr('disabled', true)
                    $('.table-box textarea').attr('disabled', true)
                })
    }
        }
    }catch(err){
        console.log(err);
    }
}



store.show_loading(true)
onMounted(async()=>{
    await get_data()
    if(order_id){
        await get_order_data()
    }
    store.show_loading(false)
})
</script>