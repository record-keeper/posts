# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-05T15:30:02.270095+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×58 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×36 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×25  [2026-08-05T15:05:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-08-05T15:05:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-08-05T15:05:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-05T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-05T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×43  [2026-08-05T12:52:29]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-08-05T11:50:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-05T06:00:07]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.69 ROI_boot95=[0.48,0.93]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=157 hit%=23.6% hit_CI[Bonf]=[15.3,34.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=49.3% hit_CI[Bonf]=[32.9,65.8]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.53 (コスト 10,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=38.2% ROI=0.92 (コスト 8,500/回収 7,820)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=31.8% ROI=0.76 (コスト 15,500/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=21.4% ROI=0.42 (コスト 9,800/回収 4,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.51MB / last modified 2026-08-05T15:29:39.454495+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
8-05 15:29:15,262 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=04&hd=20260805: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-05 15:29:26,641 [INFO] scraper: odds3t: 120/120 parsed
2026-08-05 15:29:27,744 [INFO] scraper: odds3f: 20/20 parsed
2026-08-05 15:29:28,850 [INFO] scraper: odds2t: 30/30 parsed
2026-08-05 15:29:28,851 [INFO] scraper: odds2f: 15/15 parsed
2026-08-05 15:29:29,968 [INFO] scraper: odds_win: 5/6 parsed
2026-08-05 15:29:29,968 [INFO] scraper: fetch_race 04/8: boats=6 odds=190/191
2026-08-05 15:29:29,971 [INFO] predictor: CALIBRATION_MODE=on
2026-08-05 15:29:29,971 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-05 15:29:29,975 [INFO] run_cycle: fetched 04/8 [final]: 155 combos
2026-08-05 15:29:33,620 [INFO] scraper: odds3t: 120/120 parsed
2026-08-05 15:29:34,753 [INFO] scraper: odds3f: 20/20 parsed
2026-08-05 15:29:35,853 [INFO] scraper: odds2t: 28/30 parsed
2026-08-05 15:29:35,855 [INFO] scraper: odds2f: 13/15 parsed
2026-08-05 15:29:36,924 [INFO] scraper: odds_win: 4/6 parsed
2026-08-05 15:29:36,924 [INFO] scraper: fetch_race 09/11: boats=6 odds=185/191
2026-08-05 15:29:36,927 [INFO] predictor: CALIBRATION_MODE=on
2026-08-05 15:29:36,927 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-08-05 15:29:36,931 [INFO] run_cycle: fetched 09/11 [scan]: 152 combos
2026-08-05 15:29:39,413 [WARNING] scraper: beforeinfo parse failed: jcd=01 rno=2
2026-08-05 15:29:39,413 [WARNING] run_cycle: fetch None: 01/2
2026-08-05 15:29:39,414 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 15:30:06,008 [INFO] run_cycle: === run_cycle 15:30:06 ===
2026-08-05 15:30:06,009 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 15:30:06,009 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 15:30:06,061 [INFO] predictor: Models loaded OK

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 12, 'scan': 21}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 58
  ANOMALY_SCRAPER_FAILURE_BURST: 45
  CIRCUIT_BREAKER_TRIP: 36
  CIRCUIT_BREAKER_NO_ACTION: 35
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 4
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 11 | 11,100 | 9,630 | -1,470 | 0.868 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 4,680 | -2,120 | 0.688 |
| S02_TETSUBAN | 12 | 6 | 2,400 | 1,720 | -680 | 0.717 |

## 直近アラート (24h・新しい順)
```
[15:28:21] FINAL_MISSING: {"deadline": "2026-08-05T14:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080504071458", "sid": "S00"}
[15:05:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:05:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:02:49] FINAL_MISSING: {"deadline": "2026-08-05T13:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080505051331", "sid": "S00"}
[15:01:04] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4680, "roi_7d": 0.688, "sid": "S01_NAKAANA1"}
[14:05:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:05:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:05:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:01:19] FINAL_MISSING: {"deadline": "2026-08-05T13:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080505051331", "sid": "S00"}
```

## 本日残レース: 50件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 82件 締切済
- 通知発射: scan=13 nid / final=15 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 098R | win | 1 | 0.3177 | 10.5 | 3.34 | 300 | scan=18.0 drift=-41.7% | 13:58:19 |
| S00 | 045R | win | 1 | 0.3177 | 9.5 | 3.02 | 300 | scan=10.5 drift=-9.5% | 13:52:19 |
| S01_NAKAANA1 | 055R | win | 1 | 0.5891 | 4.6 | 2.71 | 200 | scan=- drift=- | 13:28:18 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.9 drift=-10.3% | 12:35:45 |
| S00 | 053R | win | 1 | 0.5476 | 4.2 | 2.30 | 300 | scan=- drift=- | 12:29:19 |
| S00 | 094R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=6.0 drift=-13.3% | 11:56:18 |
| S01_NAKAANA1 | 172R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=- drift=- | 11:41:18 |
| S00 | 216R | win | 1 | 0.5476 | 4.7 | 2.57 | 300 | scan=4.7 drift=+0.0% | 10:51:42 |
| S02_TETSUBAN | 211R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 08:37:18 |
| S01_NAKAANA1 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.2 drift=+28.1% | 18:40:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | -3.0% | -73.3% | +107.5% | 19 | 12 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 466.7s |
| **Latency** (scan→final max) | 646.4s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 404 | 0.4605 | 0.2970 | +0.1635 | 🟡+36% | 0.2338 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4163 | 0.2626 | 0.2242 | 🔴-0.16 | 0.73 |
| S01_NAKAANA1 | win | 157 | 0.4814 | 0.2484 | 0.2393 | 🔴-0.28 | 0.729 |
| S02_TETSUBAN | win | 68 | 0.5287 | 0.5000 | 0.2467 | ✅+0.01 | 0.954 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1235 | 0.1667 | ✅-0.0432 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 156 | 0.4164 | 0.2244 | 🔴+0.1920 |
| 0.50+ | 213 | 0.5412 | 0.3615 | 🔴+0.1797 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 96 | 0.787 |
| win | <5.0 | ✅learned | 170 | 0.72 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-08-05T15:30:02.270095+09:00_