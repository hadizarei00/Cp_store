#cp_store
// pages/index.tsx import { useEffect, useState } from 'react' import { useRouter } from 'next/router'

export default function Home() { const [products, setProducts] = useState<{ id: number, amount: number, price: number }[]>([]) const router = useRouter()

useEffect(() => { fetch('/api/products') .then(res => res.json()) .then(data => setProducts(data)) }, [])

return ( <div style={{ padding: 20 }}> <h1>فروشگاه CP 🎮</h1> <ul> {products.map(p => ( <li key={p.id}> {p.amount} CP - {p.price} تومان <button onClick={() => router.push(/buy/${p.amount})}>خرید</button> </li> ))} </ul> </div> ) }

// pages/api/products.ts export default function handler(req, res) { const products = [ { id: 1, amount: 500, price: 100000 }, { id: 2, amount: 1000, price: 180000 }, { id: 3, amount: 2000, price: 350000 } ]; res.status(200).json(products); }

// pages/buy/[amount].tsx import { useRouter } from 'next/router'

export default function BuyPage() { const router = useRouter() const { amount } = router.query

const handlePayment = () => { alert(پرداخت برای ${amount} CP انجام شد!) }

return ( <div style={{ padding: 20 }}> <h1>خرید {amount} CP</h1> <button onClick={handlePayment}>پرداخت</button> </div> ) }


