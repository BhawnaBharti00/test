from fpdf import FPDF

class ColorfulResume(FPDF):
    def header(self):
        self.set_font("Helvetica", "B", 16)
        self.set_text_color(40, 40, 40)
        self.cell(0, 10, "Bhawna Bharti", ln=True, align="C")
        self.set_font("Helvetica", "", 12)
        self.cell(0, 10, "2D Animator & Creative Professional", ln=True, align="C")
        self.ln(10)

    def add_section(self, title):
        self.set_font("Helvetica", "B", 12)
        self.set_text_color(0, 102, 204)
        self.cell(0, 10, title, ln=True)
        self.set_text_color(0, 0, 0)

    def add_list(self, items):
        self.set_font("Helvetica", "", 11)
        for item in items:
            self.multi_cell(0, 6, f"- {item}")
        self.ln(2)

    def add_table(self, data):
        self.set_font("Helvetica", "", 11)
        col_widths = [50, 50, 50]
        for row in data:
            for i, item in enumerate(row):
                self.cell(col_widths[i], 6, item, border=1)
            self.ln()
        self.ln(4)

class CleanResume(ColorfulResume):
    def contact_section(self):
        self.set_font("Helvetica", "", 11)
        self.set_text_color(80, 80, 80)
        self.multi_cell(0, 6, "RANCHI, JHARKHAND    Phone: +91-9263300290")
        self.multi_cell(0, 6, "Email: bhartibhawna4488@gmail.com")
        self.multi_cell(0, 6, "Portfolio: https://bhawnacreatives.netlify.app/")
        self.multi_cell(0, 6, "LinkedIn: https://www.linkedin.com/in/bhawna-bharti-25ba2a316")
        self.multi_cell(0, 6, "Behance: https://www.behance.net/bhawnabharti48")
        self.ln(4)

# Create PDF
pdf = CleanResume()
pdf.add_page()
pdf.contact_section()

pdf.add_section("Career Objective")
pdf.set_font("Helvetica", "", 11)
pdf.multi_cell(0, 6,
    "Creative and self-driven professional with a background in 2D animation and design. Experienced in using tools like Adobe Animate, Adobe Illustrator, and DaVinci Resolve to create engaging visuals and animation. Strong command over Adobe Animate (Rigging, lip synching, walk cycle, armature & frame-by-frame). Seeking a role to deliver impactful visuals and add real value to people, along with learning."
)

pdf.add_section("Skills")
pdf.add_list([
    "Adobe Animate (2D Animation & Illustration)",
    "Adobe Illustrator (Props design)",
    "Organisational skills (Google Drive, Google Sheets, Google Docs)",
    "Storytelling & Visual Thinking",
    "AI Tools (ChatGPT, Canva AI, Leonardo AI)",
    "Team collaboration",
    "Problem-solving and Adaptability",
    "Creative Writing and Time Management"
])

pdf.add_section("Tools")
tools_data = [
    ("Adobe Animate", "Advanced", "5 Stars"),
    ("Adobe Illustrator", "Intermediate", "3 Stars"),
    ("DaVinci Resolve", "Intermediate", "3 Stars"),
    ("After Effects", "Basic (Learning)", "1 Star"),
]
pdf.add_table(tools_data)

pdf.add_section("Creative Projects")
pdf.add_list([
    "Assisted as an animator to design character and landscape for a Hindi horror YouTube channel.",
    "Fiction & Personal Blogs - Wrote short blogs on healing, self-worth, and personal reflections.",
    "Designed & developed my personal portfolio website (https://bhawnacreatives.netlify.app/)",
    "Currently working on soft ASMR-style animation project."
])

pdf.add_section("Education")
pdf.add_list([
    "St. Xavier's College, Ranchi - B.Sc. (Hons) in Botany, 2018-2021"
])

pdf.add_section("Other Experience")
pdf.add_list([
    "Freelance animation and creative writing work.",
    "Internship at IQM to animate educational and infographic work."
])

pdf.add_section("Languages")
pdf.add_list([
    "Hindi - Native",
    "English - Fluent"
])

pdf.add_section("Availability")
pdf.add_list([
    "Open to full-time, part-time, freelance, or remote opportunities",
    "Ready to start immediately"
])

# Save PDF
final_path = "Bhawna_Bharti_Resume_ColorStyled.pdf"
pdf.output(final_path)
print(f"PDF saved successfully as: {final_path}")
