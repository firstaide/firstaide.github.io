Hello world
export default function ProjectsPage() {
  const projects = [
    {
      id: "pandemic",
      title: "Pandemic Preparedness",
      description:
        "A comprehensive approach to global health security, focusing on early detection, rapid response, and effective containment of potential pandemic threats. Developed in collaboration with WHO, CDC, and local health authorities.",
      image: "/placeholder.svg?height=300&width=500&text=Pandemic+Preparedness",
      duration: "2020 - 2022",
      partners: "WHO, CDC, Local Health Authorities",
    },
    {
      id: "help-with-fees",
      title: "Help with Fees",
      description:
        "Simplifying the process of applying for fee remissions in the court and tribunal system. Redesigned the application journey to make it more accessible and user-friendly, particularly for vulnerable users.",
      image: "/placeholder.svg?height=300&width=500&text=Help+with+Fees",
      duration: "2019 - 2021",
      partners: "Legal Aid, Ministry of Justice",
    },
    {
      id: "global-billing",
      title: "Global Billing",
      description:
        "A unified payment platform that handles multi-currency transactions, tax compliance, and automated reconciliation for international businesses. The system supports operations in over 40 countries with real-time currency conversion.",
      image: "/placeholder.svg?height=300&width=500&text=Global+Billing",
      duration: "2020 - 2022",
      partners: "FinTech Alliance, Global Payment Solutions",
    },
    {
      id: "export-wins",
      title: "Export Wins",
      description:
        "Platform designed to track, validate, and report on international trade successes. Helps businesses and government agencies measure the impact of trade support programs and identify growth opportunities.",
      image: "/placeholder.svg?height=300&width=500&text=Export+Wins",
      duration: "2018 - 2020",
      partners: "Department for International Trade, Export Finance",
    },
    {
      id: "data-science",
      title: "Data Science",
      description:
        "Developing predictive models and analytical solutions across multiple sectors. Specializing in turning complex data into actionable insights that drive strategic decision-making and operational improvements.",
      image: "/placeholder.svg?height=300&width=500&text=Data+Science",
      duration: "2021 - Present",
      partners: "Various Industry Partners",
    },
    {
      id: "self-employment",
      title: "Self Employment",
      description:
        "Digital tools and resources to help independent workers manage their businesses more effectively. Provides guidance on tax compliance, financial planning, and business development for freelancers and entrepreneurs.",
      image: "/placeholder.svg?height=300&width=500&text=Self+Employment",
      duration: "2019 - 2022",
      partners: "Small Business Federation, Freelancer Association",
    },
    {
      id: "kickstart",
      title: "Kickstart",
      description:
        "Program designed to create high-quality job opportunities for young people at risk of long-term unemployment. Connects employers with talented young workers and provides subsidized employment with training and development support.",
      image: "/placeholder.svg?height=300&width=500&text=Kickstart",
      duration: "2020 - 2022",
      partners: "Department for Work and Pensions, Youth Employment UK",
    },
  ]

  return (
    <div className="container py-12 md:py-16 lg:py-24">
      <div className="space-y-4 mb-12">
        <h1 className="text-3xl font-bold tracking-tighter sm:text-4xl md:text-5xl">Projects</h1>
        <p className="max-w-[700px] text-muted-foreground md:text-xl">
          Explore my portfolio of work across various domains and disciplines.
        </p>
      </div>

      <div className="space-y-16">
        {projects.map((project) => (
          <div key={project.id} id={project.id} className="scroll-mt-20">
            <div className="grid gap-6 lg:grid-cols-[2fr_3fr] items-start">
              <div>
                <h2 className="text-2xl font-bold mb-3">{project.title}</h2>
                <p className="text-muted-foreground mb-4">{project.description}</p>
                <div className="flex flex-wrap gap-4 mb-4">
                  <div className="text-sm">
                    <span className="font-medium">Duration:</span> {project.duration}
                  </div>
                  <div className="text-sm">
                    <span className="font-medium">Partners:</span> {project.partners}
                  </div>
                </div>
                <Button variant="outline" size="sm" asChild className="group">
                  <Link href={`#${project.id}`}>
                    Learn more
                    <ArrowRight className="ml-2 h-4 w-4 group-hover:translate-x-1 transition-transform" />
                  </Link>
                </Button>
              </div>
              <div className="relative overflow-hidden rounded-lg">
                <Image
                  src={project.image || "/placeholder.svg"}
                  alt={project.title}
                  width={500}
                  height={300}
                  className="w-full object-cover transition-all hover:scale-105 aspect-[5/3]"
                />
              </div>
            </div>
            {project.id !== projects[projects.length - 1].id && <div className="my-16 h-px bg-border" />}
          </div>
        ))}
      </div>
    </div>
  )
}
