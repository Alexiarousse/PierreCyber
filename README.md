import React, { useEffect, useMemo, useState } from "react";
import { motion } from "framer-motion";
import {
  ShieldCheck,
  Gauge,
  Dumbbell,
  Moon,
  Sun,
  HeartPulse,
  Clock4,
  PhoneCall,
  Mail,
  Check,
} from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardFooter, CardHeader } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from "@/components/ui/accordion";

// Default export: a single-page Apple-like landing
export default function LandingPalisLongevite() {
  const [dark, setDark] = useState(true);
  useEffect(() => {
    const root = document.documentElement;
    if (dark) root.classList.add("dark"); else root.classList.remove("dark");
  }, [dark]);

  const calendly = "https://calendly.com/palispierre";
  const whatsapp = "https://wa.me/33698744831";
  const email = "mailto:palispierre64@gmail.com";

  // Simple fake submit for the lead magnet (to be wired later)
  const [leadEmail, setLeadEmail] = useState("");
  const onLead = (e: React.FormEvent) => {
    e.preventDefault();
    alert("Merci ! Je t'envoie la checklist par email (intégration à brancher : ESP/Notion/Make).\nEmail: " + leadEmail);
    setLeadEmail("");
  };

  // JSON-LD (SEO) — Organization + Service
  const schema = useMemo(() => ({
    "@context": "https://schema.org",
    "@type": "Organization",
    name: "Palis Longévité 40+",
    url: "https://palislongevite.com/",
    logo: "https://palislongevite.com/logo.png",
    sameAs: [whatsapp, calendly, email],
    address: { "@type": "PostalAddress", addressLocality: "Bayonne", addressCountry: "FR" },
    makesOffer: {
      "@type": "Offer",
      itemOffered: {
        "@type": "Service",
        name: "Consulting longévité masculine 40+",
        areaServed: "FR",
        audience: { "@type": "PeopleAudience", requiredMinAge: 40 },
      },
      priceCurrency: "EUR",
      priceSpecification: [
        { "@type": "UnitPriceSpecification", name: "Démarrage 1 mois", price: 190 },
        { "@type": "UnitPriceSpecification", name: "Optimisation 3 mois", price: 490 },
        { "@type": "UnitPriceSpecification", name: "Transformation 6 mois", price: 2000 },
      ],
      availability: "https://schema.org/InStock",
    },
  }), []);

  return (
    <div className="min-h-screen bg-white text-neutral-900 antialiased dark:bg-neutral-950 dark:text-neutral-50">
      {/* Head-like meta (works in preview; move to <Head> in Next.js) */}
      <title>Palis Longévité 40+ — Clair. Fort. Stable.</title>
      <meta name="description" content="Énergie, libido, sommeil et force — en 30, 90 ou 180 jours. Consulting longévité masculine 40+ (Bayonne)." />
      <meta property="og:title" content="Palis Longévité 40+" />
      <meta property="og:description" content="Méthode 4 piliers + routines compactes. Garantie remobilisation 2 semaines." />
      <script type="application/ld+json" dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }} />

      {/* Gradient background ornaments */}
      <div className="pointer-events-none absolute inset-0 overflow-hidden">
        <div className="absolute -top-40 -left-40 h-[36rem] w-[36rem] rounded-full bg-gradient-to-br from-sky-600/25 via-sky-500/10 to-transparent blur-3xl dark:from-sky-500/25 dark:via-sky-400/10" />
        <div className="absolute -bottom-40 -right-40 h-[36rem] w-[36rem] rounded-full bg-gradient-to-br from-amber-400/20 via-amber-300/10 to-transparent blur-3xl" />
      </div>

      {/* Nav */}
      <header className="sticky top-0 z-50 backdrop-blur-sm bg-white/60 dark:bg-neutral-950/60 border-b border-neutral-200/60 dark:border-neutral-800">
        <div className="mx-auto max-w-7xl px-4 py-3 flex items-center justify-between">
          <div className="flex items-center gap-2">
            <div className="flex h-9 w-9 items-center justify-center rounded-full bg-neutral-900 dark:bg-neutral-100 text-white dark:text-neutral-900 ring-1 ring-white/10 shadow">
              <span className="text-sm font-bold">P+</span>
            </div>
            <div className="text-sm leading-tight">
              <div className="font-semibold tracking-tight">Palis Longévité 40+</div>
              <div className="text-neutral-500 dark:text-neutral-400 text-xs">Bayonne • FR</div>
            </div>
          </div>
          <div className="flex items-center gap-2">
            <Button variant="ghost" className="hidden md:inline-flex" onClick={() => window.open(calendly, "_blank")}>Réserver</Button>
            <Button className="hidden md:inline-flex" onClick={() => window.open(whatsapp, "_blank")}>WhatsApp</Button>
            <Button variant="ghost" size="icon" onClick={() => setDark(v => !v)} aria-label="Basculer thème">
              {dark ? <Sun className="h-5 w-5" /> : <Moon className="h-5 w-5" />}
            </Button>
          </div>
        </div>
      </header>

      {/* Hero */}
      <section className="relative mx-auto max-w-7xl px-4 pt-16 pb-12 md:pt-24 md:pb-20">
        <div className="grid items-center gap-10 md:grid-cols-2">
          <div>
            <motion.h1 initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6 }}
              className="text-4xl md:text-6xl font-semibold tracking-tight">
              <span className="bg-gradient-to-b from-neutral-900 to-neutral-600 bg-clip-text text-transparent dark:from-neutral-100 dark:to-neutral-400">Clair. Fort. Stable.</span>
            </motion.h1>
            <p className="mt-4 text-neutral-600 dark:text-neutral-300 text-lg">
              Énergie, libido, sommeil et force — en 30, 90 ou 180 jours. Programmes conçus pour des vies exigeantes.
            </p>
            <div className="mt-6 flex flex-col sm:flex-row gap-3">
              <Button size="lg" className="h-12 px-6" onClick={() => window.open(calendly, "_blank")}>Réserver un appel (20–30 min)</Button>
              <Button size="lg" variant="outline" className="h-12 px-6" onClick={() => document.getElementById("lead").scrollIntoView({behavior:'smooth'})}>Checklist Sommeil (10 min)</Button>
            </div>
            <div className="mt-6 flex items-center gap-4 text-sm text-neutral-500 dark:text-neutral-400">
              <div className="flex items-center gap-2"><ShieldCheck className="h-4 w-4" /> Garantie remobilisation 2 semaines</div>
              <div className="flex items-center gap-2"><Clock4 className="h-4 w-4" /> Réponse sous 24h</div>
            </div>
          </div>
          {/* Placeholder visual — black & white studio style */}
          <div className="relative aspect-[4/3] w-full overflow-hidden rounded-3xl border border-neutral-200/60 dark:border-neutral-800 shadow-lg bg-gradient-to-br from-neutral-900 to-neutral-700 dark:from-neutral-800 dark:to-neutral-900">
            <div className="absolute inset-0 opacity-20 bg-[radial-gradient(ellipse_at_center,rgba(255,255,255,0.3),rgba(0,0,0,0)_60%)]" />
            <div className="absolute bottom-4 left-4 text-neutral-300 text-xs tracking-wide uppercase">Studio N&B • placeholder (à remplacer)</div>
          </div>
        </div>
      </section>

      {/* Value props / Méthode 4 piliers */}
      <section className="mx-auto max-w-7xl px-4 py-12 md:py-16">
        <div className="grid gap-6 md:grid-cols-4">
          <ValueCard icon={<Moon className="h-5 w-5" />} title="Sommeil & rythme" text="Ancrage horaire, lumière, température, rituels anti-cortisol." />
          <ValueCard icon={<HeartPulse className="h-5 w-5" />} title="Nutrition & métabolisme" text="Protéines suffisantes, lipides de qualité, timing glucidique." />
          <ValueCard icon={<Dumbbell className="h-5 w-5" />} title="Force & cardio" text="3 séances efficaces + Zone 2 et VO2max." />
          <ValueCard icon={<Gauge className="h-5 w-5" />} title="Stress & libido" text="Respiration, charge allostatique, rituels de couple." />
        </div>
      </section>

      {/* Offres */}
      <section id="offres" className="mx-auto max-w-7xl px-4 py-12 md:py-16">
        <div className="mb-8 text-center">
          <h2 className="text-2xl md:text-4xl font-semibold tracking-tight">Trois niveaux, un même standard de qualité</h2>
          <p className="mt-2 text-neutral-600 dark:text-neutral-300">Choisis le rythme qui colle à ta vie. Paiement Stripe sécurisé.</p>
        </div>
        <div className="grid gap-6 md:grid-cols-3">
          <PlanCard
            title="Démarrage"
            price="190€"
            ribbon="1 mois"
            bullets={["Audit & plan 4 semaines","Routine 3×/semaine + rituels","Tableur de suivi + 2 points/sem"]}
            onClick={() => window.open(calendly, "_blank")}
          />
          <PlanCard
            featured
            title="Optimisation"
            price="490€"
            ribbon="3 mois"
            bullets={["Alimentation cyclique & compléments","Musculation progressive + HIIT","Ajustements bi-hebdo + 1h/mois"]}
            onClick={() => window.open(calendly, "_blank")}
            note="Options de paiement en plusieurs fois disponibles"
          />
          <PlanCard
            title="Transformation"
            price="2000€"
            ribbon="6 mois"
            bullets={["Cardio longévité (Zone 2 & VO2max)","Récupération, focus mental, discipline","Support illimité + rapport final"]}
            onClick={() => window.open(calendly, "_blank")}
            note="Options de paiement en 3x sur demande"
          />
        </div>
      </section>

      {/* Réassurance / Indicateurs */}
      <section className="mx-auto max-w-7xl px-4 py-12 md:py-16">
        <div className="grid gap-6 md:grid-cols-3">
          <Reassure title="Mesurable" text="Énergie (1–10), sommeil (profond/lever), libido (fréquence/envie), FC repos, tour de taille, force de préhension." />
          <Reassure title="Adapté à la vraie vie" text="Plans compacts et itératifs. Déplacements & famille pris en compte." />
          <Reassure title="Garantie 2 semaines" text="Si le plan 30 jours est appliqué sans amélioration de marqueurs simples, prolongation offerte." />
        </div>
      </section>

      {/* Lead magnet */}
      <section id="lead" className="mx-auto max-w-3xl px-4 py-12 md:py-16">
        <Card className="overflow-hidden border-neutral-200 dark:border-neutral-800">
          <div className="bg-gradient-to-br from-neutral-900 to-neutral-700 p-6 text-neutral-100">
            <h3 className="text-xl font-semibold tracking-tight">Checklist Sommeil Profond (10 minutes)</h3>
            <p className="text-sm opacity-80">Les 7 leviers concrets pour dormir mieux dès cette semaine. Reçois le PDF par email.</p>
          </div>
          <CardContent className="p-6">
            <form onSubmit={onLead} className="flex flex-col gap-3 sm:flex-row">
              <Input required type="email" placeholder="Ton email" value={leadEmail} onChange={(e) => setLeadEmail(e.target.value)} />
              <Button type="submit">Recevoir le PDF</Button>
            </form>
            <p className="mt-2 text-xs text-neutral-500 dark:text-neutral-400">Pas de spam. Désinscription en 1 clic.</p>
          </CardContent>
        </Card>
      </section>

      {/* FAQ */}
      <section className="mx-auto max-w-4xl px-4 py-12 md:py-16">
        <h3 className="text-2xl font-semibold tracking-tight mb-4">FAQ</h3>
        <Accordion type="single" collapsible className="divide-y divide-neutral-200 dark:divide-neutral-800">
          <AccordionItem value="q1">
            <AccordionTrigger>Est-ce médical ?</AccordionTrigger>
            <AccordionContent>Non — il s’agit de coaching d’hygiène de vie. Toute décision médicale relève de ton médecin.</AccordionContent>
          </AccordionItem>
          <AccordionItem value="q2">
            <AccordionTrigger>Faut-il une salle de sport ?</AccordionTrigger>
            <AccordionContent>Non. Programmes maison possibles. Une salle peut accélérer la progression, mais n’est pas obligatoire.</AccordionContent>
          </AccordionItem>
          <AccordionItem value="q3">
            <AccordionTrigger>Combien de temps par semaine ?</AccordionTrigger>
            <AccordionContent>En moyenne 3× 30–45 min + de micro-rituels de 5–10 min.</AccordionContent>
          </AccordionItem>
          <AccordionItem value="q4">
            <AccordionTrigger>Proposes-tu le paiement en plusieurs fois ?</AccordionTrigger>
            <AccordionContent>Oui, via Stripe, pour les programmes 490€ et 2000€ (détails confirmés pendant l’appel).</AccordionContent>
          </AccordionItem>
        </Accordion>
      </section>

      {/* CTA final */}
      <section className="mx-auto max-w-7xl px-4 pb-16">
        <Card className="border-neutral-200 dark:border-neutral-800 overflow-hidden">
          <div className="p-8 bg-gradient-to-br from-sky-600 to-sky-700 text-white">
            <h3 className="text-2xl md:text-3xl font-semibold tracking-tight">Prêt à redevenir clair, fort et stable ?</h3>
            <p className="opacity-90 mt-1">Réserve un appel découverte de 20–30 minutes. Réponse sous 24h.</p>
            <div className="mt-6 flex flex-wrap gap-3">
              <Button size="lg" variant="secondary" onClick={() => window.open(calendly, "_blank")}>Réserver un appel</Button>
              <Button size="lg" variant="outline" onClick={() => window.open(whatsapp, "_blank")}>
                Parler sur WhatsApp
              </Button>
            </div>
          </div>
          <CardFooter className="flex items-center gap-4 p-6 text-sm">
            <div className="flex items-center gap-2"><PhoneCall className="h-4 w-4" />06 98 74 48 31</div>
            <div className="flex items-center gap-2"><Mail className="h-4 w-4" />palispierre64@gmail.com</div>
            <div className="ml-auto text-neutral-500 dark:text-neutral-400">Bayonne • FR</div>
          </CardFooter>
        </Card>
      </section>

      {/* Footer */}
      <footer className="border-t border-neutral-200/60 dark:border-neutral-800">
        <div className="mx-auto max-w-7xl px-4 py-8 text-sm text-neutral-500 dark:text-neutral-400 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
          <div>© {new Date().getFullYear()} Palis Longévité 40+ — Coaching hygiène de vie, non médical.</div>
          <div className="flex gap-4">
            <a className="hover:underline" href="#">Mentions légales</a>
            <a className="hover:underline" href="#">CGV</a>
            <a className="hover:underline" href="#">Confidentialité</a>
          </div>
        </div>
      </footer>
    </div>
  );
}

function ValueCard({ icon, title, text }: { icon: React.ReactNode; title: string; text: string }) {
  return (
    <Card className="border-neutral-200 dark:border-neutral-800">
      <CardHeader className="flex flex-row items-center gap-3">
        <div className="h-9 w-9 rounded-full bg-neutral-900 text-white dark:bg-neutral-100 dark:text-neutral-900 flex items-center justify-center">
          {icon}
        </div>
        <div className="font-medium">{title}</div>
      </CardHeader>
      <CardContent className="pt-0 text-neutral-600 dark:text-neutral-300">{text}</CardContent>
    </Card>
  );
}

function PlanCard({ featured, title, price, ribbon, bullets, onClick, note }:{ featured?: boolean; title: string; price: string; ribbon: string; bullets: string[]; onClick: () => void; note?: string; }) {
  return (
    <Card className={`relative overflow-hidden border-neutral-200 dark:border-neutral-800 ${featured ? 'ring-2 ring-sky-600 dark:ring-sky-500' : ''}`}>
      <div className="absolute right-0 top-0 rounded-bl-xl bg-sky-600 px-3 py-1 text-xs font-semibold text-white">{ribbon}</div>
      <CardHeader>
        <div className="flex items-baseline justify-between">
          <h3 className="text-xl font-semibold tracking-tight">{title}</h3>
          <div className="text-2xl font-semibold">{price}</div>
        </div>
      </CardHeader>
      <CardContent className="grid gap-2">
        {bullets.map((b, i) => (
          <div key={i} className="flex items-start gap-2 text-neutral-700 dark:text-neutral-300">
            <Check className="mt-1 h-4 w-4 text-amber-500" />
            <span>{b}</span>
          </div>
        ))}
        {note && <p className="text-xs text-neutral-500 dark:text-neutral-400 mt-1">{note}</p>}
      </CardContent>
      <CardFooter>
        <Button onClick={onClick} className="w-full">Commencer</Button>
      </CardFooter>
    </Card>
  );
}

// NEW: Reassure component was missing and caused a ReferenceError.
// It mirrors ValueCard but with a simpler layout for reassurance items.
function Reassure({ title, text }: { title: string; text: string }) {
  return (
    <Card className="border-neutral-200 dark:border-neutral-800">
      <CardHeader>
        <h4 className="text-lg font-medium tracking-tight">{title}</h4>
      </CardHeader>
      <CardContent className="pt-0 text-neutral-600 dark:text-neutral-300">
        {text}
      </CardContent>
    </Card>
  );
}
