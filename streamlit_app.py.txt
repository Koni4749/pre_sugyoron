import streamlit as st

# --- 페이지 설정 ---
st.set_page_config(
    page_title="홍길동 포트폴리오",
    page_icon="👤",
    layout="wide",
    initial_sidebar_state="expanded"
)

# --- 커스텀 CSS (React 디자인 재현) ---
st.markdown("""
    <style>
    /* 전체 배경 및 폰트 */
    .stApp {
        background-color: #f8fafc;
    }
    
    /* 사이드바 프로필 스타일 */
    [data-testid="stSidebar"] {
        background-color: white;
        border-right: 1px solid #e2e8f0;
    }
    
    .profile-card {
        text-align: center;
        padding: 20px 0;
    }
    
    .profile-img {
        width: 120px;
        height: 120px;
        background: linear-gradient(135deg, #3b82f6, #4f46e5);
        border-radius: 24px;
        margin: 0 auto 15px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: white;
        font-size: 40px;
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    }
    
    /* 태그 스타일 */
    .skill-tag {
        display: inline-block;
        padding: 4px 10px;
        background-color: #f1f5f9;
        color: #475569;
        border-radius: 6px;
        font-size: 12px;
        font-weight: 600;
        margin: 2px;
    }
    
    /* 프로젝트 카드 스타일 */
    .project-card {
        background-color: white;
        padding: 24px;
        border-radius: 16px;
        border: 1px solid #e2e8f0;
        transition: all 0.3s ease;
        margin-bottom: 20px;
    }
    
    .project-card:hover {
        border-color: #3b82f6;
        box-shadow: 0 10px 25px -5px rgba(59, 130, 246, 0.1);
    }
    </style>
""", unsafe_allow_html=True)

# --- 데이터 정의 ---
profile = {
    "name": "홍길동",
    "role": "Full-Stack Developer",
    "email": "gildong@example.com",
    "phone": "010-1234-5678",
    "location": "서울시 강남구",
    "bio": "데이터와 사용자 경험을 연결하는 가교 역할을 하는 개발자입니다. 효율적인 코드와 깔끔한 UI를 지향하며, 새로운 기술을 학습하고 공유하는 것을 즐깁니다.",
    "skills": ["React", "Node.js", "TypeScript", "Python", "Tailwind CSS", "PostgreSQL"]
}

# --- 사이드바 구성 ---
with st.sidebar:
    st.markdown(f"""
        <div class="profile-card">
            <div class="profile-img">👤</div>
            <h1 style='font-size: 24px; margin-bottom: 5px;'>{profile['name']}</h1>
            <p style='color: #3b82f6; font-weight: 500;'>{profile['role']}</p>
        </div>
    """, unsafe_allow_html=True)
    
    st.divider()
    
    st.markdown("### 📞 Contact")
    st.caption(f"📧 {profile['email']}")
    st.caption(f"📱 {profile['phone']}")
    st.caption(f"📍 {profile['location']}")
    
    st.divider()
    
    st.markdown("### 🛠️ Tech Skills")
    skill_html = "".join([f'<span class="skill-tag">{s}</span>' for s in profile['skills']])
    st.markdown(f'<div>{skill_html}</div>', unsafe_allow_html=True)
    
    st.divider()
    
    if st.button("📄 Resume Download", use_container_width=True):
        st.info("이력서 파일 링크를 연결하세요.")

# --- 메인 콘텐츠 (탭 이동) ---
selected_tab = st.selectbox(
    "메뉴 선택",
    ["About", "Experience", "Projects"],
    label_visibility="collapsed"
)

st.markdown("<br>", unsafe_allow_html=True)

if selected_tab == "About":
    st.header(f"안녕하세요, {profile['name']}입니다. 👋")
    st.write(profile['bio'])
    
    col1, col2 = st.columns(2)
    with col1:
        st.info("**Clean Architecture**\n\n유지보수가 용이하고 확장 가능한 코드 구조를 설계하는 데 집중합니다.")
    with col2:
        st.success("**Modern Tech Stack**\n\n최신 프레임워크와 도구들을 적극적으로 도입하여 개발 생산성을 높입니다.")

elif selected_tab == "Experience":
    st.header("💼 Career Experience")
    
    experiences = [
        {"company": "테크 이노베이션", "role": "선임 개발자", "period": "2022.03 - 현재", "desc": "클라우드 기반 협업 솔루션 프론트엔드 아키텍처 설계 및 개발 총괄."},
        {"company": "미래 소프트", "role": "주니어 개발자", "period": "2020.01 - 2022.02", "desc": "사내 ERP 시스템 유지보수 및 신규 모듈 개발."}
    ]
    
    for exp in experiences:
        with st.container():
            c1, c2 = st.columns([3, 1])
            c1.subheader(exp['company'])
            c2.markdown(f"**{exp['period']}**")
            st.markdown(f"*{exp['role']}*")
            st.write(exp['desc'])
            st.divider()

elif selected_tab == "Projects":
    st.header("🚀 Key Projects")
    
    projects = [
        {
            "title": "AI 기반 수학 학습 플랫폼",
            "period": "2024.01 - 2024.03",
            "desc": "Gemini API를 활용하여 학생들의 오답을 분석하고 맞춤형 힌트를 제공하는 웹 애플리케이션입니다.",
            "tags": ["React", "Gemini API", "Tailwind"]
        },
        {
            "title": "실시간 협업 화이트보드",
            "period": "2023.10 - 2023.12",
            "desc": "WebSocket을 활용하여 여러 사용자가 동시에 드로잉하고 아이디어를 공유할 수 있는 툴입니다.",
            "tags": ["Node.js", "Socket.io", "Canvas API"]
        }
    ]
    
    col_p1, col_p2 = st.columns(2)
    for i, proj in enumerate(projects):
        target_col = col_p1 if i % 2 == 0 else col_p2
        with target_col:
            st.markdown(f"""
                <div class="project-card">
                    <h3 style='margin-top:0;'>{proj['title']}</h3>
                    <p style='font-size: 14px; color: #64748b;'>{proj['desc']}</p>
                    <div style='margin-top: 15px;'>
                        {" ".join([f'<span class="skill-tag">{t}</span>' for t in proj['tags']])}
                    </div>
                </div>
            """, unsafe_allow_html=True)

# --- 하단 CTA ---
st.markdown("<br><br>", unsafe_allow_html=True)
st.markdown("""
    <div style='background-color: #0f172a; padding: 40px; border-radius: 24px; text-align: center; color: white;'>
        <h2>함께 멋진 프로젝트를 만들어볼까요?</h2>
        <p style='color: #94a3b8;'>새로운 도전과 협업은 언제나 환영입니다.</p>
        <div style='margin-top: 20px;'>
            <a href='#' style='color: white; margin: 0 10px;'>Github</a>
            <a href='#' style='color: white; margin: 0 10px;'>LinkedIn</a>
        </div>
    </div>
""", unsafe_allow_html=True)
